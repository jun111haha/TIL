## **1. 계단오르기**

- 설명

철수는 계단을 오를 때 한 번에 한 계단 또는 두 계단씩 올라간다. 만약 총 4계단을 오른다면 그 방법의 수는

1+1+1+1, 1+1+2, 1+2+1, 2+1+1, 2+2 로 5가지이다.

그렇다면 총 N계단일 때 철수가 올라갈 수 있는 방법의 수는 몇 가지인가?

![https://cote.inflearn.com/public/upload/5616100fde.jpg](https://cote.inflearn.com/public/upload/5616100fde.jpg)

- 입력

첫째 줄은 계단의 개수인 자연수 N(3≤N≤35)이 주어집니다.

- 출력

첫 번째 줄에 올라가는 방법의 수를 출력합니다.

```java
package Main;

import java.util.*;

/*
* 입력 예시
7

* 출력예시
* 21
* */

class Main {
    static int[] dy;
    public static int solution(int n){
        dy[1] = 1;
        dy[2] = 2;

        for(int i=3; i<=n; i++){
            dy[i] = dy[i - 2] + dy[i - 1];
        }

        return dy[n];
    }

    public static void main(String[] args){
      Scanner scanner = new Scanner(System.in);
      int x = scanner.nextInt();
      dy = new int[x + 1];

      System.out.println(solution(x));
    }
}
```

## **2. 돌다리 건너기**

- 설명

철수는 학교에 가는데 개울을 만났습니다. 개울은 N개의 돌로 다리를 만들어 놓았습니다.

철수는 돌 다리를 건널 때 한 번에 한 칸 또는 두 칸씩 건너뛰면서 돌다리를 건널 수 있습니다.

철수가 개울을 건너는 방법은 몇 가지일까요?

![https://cote.inflearn.com/public/upload/d7efa0719e.jpg](https://cote.inflearn.com/public/upload/d7efa0719e.jpg)

- 입력

첫째 줄은 돌의 개수인 자연수 N(3≤N≤35)이 주어집니다.

- 출력

첫 번째 줄에 개울을 건너는 방법의 수를 출력합니다.

```java
package Main;

import java.util.*;

/*
* 입력 예시
7

* 출력예시
* 34
* */

class Main {
    static int[] dy;
    public static int solution(int n){
        dy[1] = 1;
        dy[2] = 2;

        for(int i=3; i<=n+1; i++){
            dy[i] = dy[i - 2] + dy[i - 1];
        }

        return dy[n+1];
    }

    public static void main(String[] args){
      Scanner scanner = new Scanner(System.in);
      int x = scanner.nextInt();
      dy = new int[x+2];

      System.out.println(solution(x));
    }
}
```

## **3. 최대 부분 증가수열**

- 설명

N개의 자연수로 이루어진 수열이 주어졌을 때, 그 중에서 가장 길게 증가하는(작은 수에서 큰 수로) 원소들의 집합을 찾는 프로그램을 작성하라.

예를 들어, 원소가 2, 7, 5, 8, 6, 4, 7, 12, 3 이면 가장 길게 증가하도록 원소들을 차례대로 뽑아내면 2, 5, 6, 7, 12를 뽑아내어

길이가 5인 최대 부분 증가수열을 만들 수 있다.

- 입력

첫째 줄은 입력되는 데이터의 수 N(3≤N≤1,000, 자연수)를 의미하고,

둘째 줄은 N개의 입력데이터들이 주어진다.

- 출력

첫 번째 줄에 부분증가수열의 최대 길이를 출력한다.

```java
package Main;

import java.util.*;

/*
* 입력 예시
8
5 3 7 8 6 2 9 4

* 출력예시
* 4
* */

class Main {
    static int[] dy;
    public static int solution(int [] arr){
        int answer = 0;
        dy = new int[arr.length];
        dy[0] = 1;

        for(int i=1; i<arr.length; i++){
            int max = 0;
            //i 전 까지 도는 반복문
            for(int j=i-1; j>=0; j--){
                if(arr[j]<arr[i] && dy[j] > max){
                    //dy[j] 의 최대길이의 값
                    max = dy[j];
                }
                //if 문을 안타면 앞에 항이 없다는 뜻 max=0 이니까 +1 해줘서 다이나믹값을 1로 유지
                dy[i] = max +1;
                answer = Math.max(answer, dy[i]);
            }
        }
        return answer;
    }

    public static void main(String[] args){
      Scanner scanner = new Scanner(System.in);
      int n = scanner.nextInt();
      int[] arr = new int[n];
      for(int i =0; i<n; i++){
          arr[i] = scanner.nextInt();
      }

      System.out.println(solution(arr));
    }
}
```

## **4. 가장 높은 탑 쌓기**

- 설명

밑면이 정사각형인 직육면체 벽돌들을 사용하여 탑을 쌓고자 한다. 탑은 벽돌을 한 개씩 아래에서 위로 쌓으면서 만들어 간다.

아래의 조건을 만족하면서 가장 높은 탑을 쌓을 수 있는 프로그램을 작성하시오.

(조건1) 벽돌은 회전시킬 수 없다. 즉, 옆면을 밑면으로 사용할 수 없다.

(조건2) 밑면의 넓이가 같은 벽돌은 없으며, 또한 무게가 같은 벽돌도 없다.

(조건3) 벽돌들의 높이는 같을 수도 있다.

(조건4) 탑을 쌓을 때 밑면이 좁은 벽돌 위에 밑면이 넓은 벽돌은 놓을 수 없다.

(조건5) 무게가 무거운 벽돌을 무게가 가벼운 벽돌 위에 놓을 수 없다.

- 입력

입력 파일의 첫째 줄에는 입력될 벽돌의 수가 주어진다. 입력으로 주어지는 벽돌의 수는 최대 100개이다.

둘째 줄부터는 각 줄에 한 개의 벽돌에 관한 정보인 벽돌 밑면의 넓이, 벽돌의 높이 그리고 무게가 차례대로 양의 정수로 주어진다.

각 벽돌은 입력되는 순서대로 1부터 연속적인 번호를 가진다. 벽돌의 넓이, 높이 무게는 10,000보다 작거나 같은 자연수이다.

- 출력

첫 번째 줄에 가장 높이 쌓을 수 있는 탑의 높이를 출력한다.

```java
package Main;

import java.util.*;

/*
* 입력 예시
8
5 3 7 8 6 2 9 4

* 출력예시
* 4
* */

class Brick implements Comparable<Brick>{
    //벽돌의 넓이 , 높이 , 무게
    int s;
    int h;
    int w;
    Brick(int s, int h, int w){
        this.s = s;
        this.h = h;
        this.w = w;
    }

    @Override
    public int compareTo(Brick o) {
        //넓이에 의해서 내림차순
        return o.s - this.s;
    }
}

class Main {
    static int[] dy;
    public static int solution(ArrayList<Brick> arr){
        int answer = 0;
        Collections.sort(arr);
        dy[0] = arr.get(0).h;
        answer = dy[0];

        //높은 탑 최대부분증가수열
        for(int i=1; i<arr.size(); i++){
            int max_h = 0;
            for(int j=i-1; j>=0; j--){
                if(arr.get(j).w > arr.get(i).w && dy[j] > max_h){
                    max_h = dy[j];
                }
            }
            dy[i] = max_h + arr.get(i).h;
            answer = Math.max(answer, dy[i]);
        }

        return answer;
    }

    public static void main(String[] args){
      Scanner scanner = new Scanner(System.in);
      int n = scanner.nextInt();
      dy = new int[n];
      ArrayList<Brick> arr = new ArrayList<>();
      for(int i =0; i<n; i++){
          int a = scanner.nextInt();
          int b = scanner.nextInt();
          int c = scanner.nextInt();
          arr.add(new Brick(a,b,c));
      }

      System.out.println(solution(arr));
    }
}
```

## **5. 동전교환(냅색 알고리즘)**

- 설명

다음과 같이 여러 단위의 동전들이 주어져 있을때 거스름돈을 가장 적은 수의 동전으로 교환해주려면 어떻게 주면 되는가?

각 단위의 동전은 무한정 쓸 수 있다.

- 입력

첫 번째 줄에는 동전의 종류개수 N(1<=N<=50)이 주어진다.

두 번째 줄에는 N개의 동전의 종류가 주어지고, 그 다음줄에 거슬러 줄 금액 M(1<=M<=500)이 주어진다.

각 동전의 종류는 100원을 넘지 않는다.

- 출력

첫 번째 줄에 거슬러 줄 동전의 최소개수를 출력한다.

```java
package Main;

import java.util.*;

/*
* 입력 예시
3
1 2 5
15

* 출력예시
* 3
* */

class Main {
    static int[] dy;
    static int n, m;
    public static int solution(int[] coin){
        //dy 를 큰숫자로 다 초기화
        Arrays.fill(dy , Integer.MAX_VALUE);
        dy[0] = 0;
        /*
        * 동전의 갯수 n
        * 거슬러줄 갯수 m
        * j 는 동전의 금액부터 거슬러줄 금액까지 dy 의 값을 기존값보다 작으면 교체
        * dy[i]: i 금액을 만드는데 드는 최소 동전 개수
        * */
        for(int i=0; i<n; i++){
            /*
            * 2 원부터 돈다고 치면 j - coin[i]
            * j 원을 만드는데, coin[i] 단위를 한번 사용
            * 그 금액만큼 뺀다. +1 하는이유? 동전갯수니까.
            * */
            for(int j=coin[i]; j<=m; j++){
                dy[j] = Math.min(dy[j], dy[j - coin[i]] + 1);
            }
        }
        return dy[m];

    }
    public static void main(String[] args){
      Scanner scanner = new Scanner(System.in);
      n = scanner.nextInt();
      int[] arr = new int[n];
      for(int i =0; i<n; i++){
          arr[i] = scanner.nextInt();
      }

      m = scanner.nextInt();
      dy = new int[m + 1];

      System.out.println(solution(arr));
    }
}
```

## **6. 최대점수 구하기(냅색 알고리즘)**

- 설명

이번 정보올림피아드대회에서 좋은 성적을 내기 위하여 현수는 선생님이 주신 N개의 문제를 풀려고 합니다.

각 문제는 그것을 풀었을 때 얻는 점수와 푸는데 걸리는 시간이 주어지게 됩니다.

제한시간 M안에 N개의 문제 중 최대점수를 얻을 수 있도록 해야 합니다.

(해당문제는 해당시간이 걸리면 푸는 걸로 간주한다, 한 유형당 한개만 풀 수 있습니다.)

- 입력

첫 번째 줄에 문제의 개수N(1<=N<=50)과 제한 시간 M(10<=M<=300)이 주어집니다.

두 번째 줄부터 N줄에 걸쳐 문제를 풀었을 때의 점수와 푸는데 걸리는 시간이 주어집니다.

- 출력

첫 번째 줄에 제한 시간안에 얻을 수 있는 최대 점수를 출력합니다.

```java
package Main;

import java.util.*;

/*
* 입력 예시
5 20
10 5
25 12
15 8
6 3
7 4

* 출력예시
* 41
* */

class Main {
    public static void main(String[] args){
      Scanner scanner = new Scanner(System.in);
      int n = scanner.nextInt();
      int m = scanner.nextInt();
      int[] dy = new int[m + 1];

      for(int i =0; i<n; i++){
          int ps = scanner.nextInt(); //문제를 풀고 얻을점수
          int pt = scanner.nextInt(); //문제를 푸는시간
          /*
          * 뒤에서부터 도는이유? 앞에서 부터 돌면 문제를 두번푸는현상 발생
          * 뒤에서부터 돌아야 문제를 한번 푼다는 가정 성립.
          * */
          for(int j =m; j>=pt; j--){
              dy[j] = Math.max(dy[j], dy[j - pt] + ps);
          }
      }
        System.out.println(dy[m]);
    }
}
```
