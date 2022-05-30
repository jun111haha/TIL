### 1. 두 배열 합치기(**Two pointers**)

- 설명

오름차순으로 정렬이 된 두 배열이 주어지면 두 배열을 오름차순으로 합쳐 출력하는 프로그램을 작성하세요.

- 입력

첫 번째 줄에 첫 번째 배열의 크기 N(1<=N<=100)이 주어집니다.

두 번째 줄에 N개의 배열 원소가 오름차순으로 주어집니다.

세 번째 줄에 두 번째 배열의 크기 M(1<=M<=100)이 주어집니다.

네 번째 줄에 M개의 배열 원소가 오름차순으로 주어집니다.

각 리스트의 원소는 int형 변수의 크기를 넘지 않습니다.

- 출력

오름차순으로 정렬된 배열을 출력합니다.

```java
package Main;

import java.util.*;
/*
* 입력 예시 :
3
1 3 5
5
2 3 6 7 9

	* 출력 예시 : 1 2 3 3 5 6 7 9
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num1 = scanner.nextInt();
        int [] list1 = new int[num1];
        for(int i=0; i<list1.length; i++){
            list1[i] = scanner.nextInt();
        }

        int num2 = scanner.nextInt();
        int [] list2 = new int[num2];
        for(int i=0; i<list2.length; i++){
            list2[i] = scanner.nextInt();
        }

        for(int x : solution(num1, num2, list1, list2)){
            System.out.print(x + " ");
        }

    }

    public static ArrayList<Integer> solution(int num1, int num2, int[] list1, int[] list2){
        ArrayList<Integer> answer = new ArrayList<>();

        int p1 =0, p2 = 0;
        while (p1 < num1 && p2 < num2){
            if(list1[p1] < list2[p2]){
                answer.add(list1[p1++]); //후위증감 -> answer에 add가 먼저되고 증감.
            }else{
                answer.add(list2[p2++]);
            }
        }

        while (p1 < num1){
            answer.add(list1[p1++]);
        }

        while (p2 < num2){
            answer.add(list2[p2++]);
        }
        return answer;
    }
}
```

- 풀이

시간 복잡도 O(nLogn) ⇒ O(n) 자료가 커질수록 엄청난 차이가 남.

while 문을 통해서 p1 과 p2 를 통해서 num1 , num2 과 비교한후 answer 에 add →

p1 이 남아있으면 while 다시 돌리고 p2 가 남아있으면 while 문 돌리면됨.

---

### 2. 공통원소 구하기(**Two pointers**)

- 설명

A, B 두 개의 집합이 주어지면 두 집합의 공통 원소를 추출하여 오름차순으로 출력하는 프로그램을 작성하세요.

- 입력

첫 번째 줄에 집합 A의 크기 N(1<=N<=30,000)이 주어집니다.

두 번째 줄에 N개의 원소가 주어집니다. 원소가 중복되어 주어지지 않습니다.

세 번째 줄에 집합 B의 크기 M(1<=M<=30,000)이 주어집니다.

네 번째 줄에 M개의 원소가 주어집니다. 원소가 중복되어 주어지지 않습니다.

각 집합의 원소는 1,000,000,000이하의 자연수입니다.

- 출력

두 집합의 공통원소를 오름차순 정렬하여 출력합니다.

1. 예시1(내풀이)

```java
package Main;

import java.util.*;
/*
* 입력 예시 :
5
1 3 9 5 2
5
3 2 5 7 8

* 출력 예시 : 2 3 5
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num1 = scanner.nextInt();
        int [] list1 = new int[num1];
        for(int i=0; i<list1.length; i++){
            list1[i] = scanner.nextInt();
        }

        int num2 = scanner.nextInt();
        int [] list2 = new int[num2];
        for(int i=0; i<list2.length; i++){
            list2[i] = scanner.nextInt();
        }

        for(int x : solution(num1, num2, list1, list2)){
            System.out.print(x + " ");
        }

    }

    public static ArrayList<Integer> solution(int num1, int num2, int[] list1, int[] list2){
        ArrayList<Integer> answer = new ArrayList<>();

        for(int i=0; i<num1; i++){
            for(int j=0; j<num2; j++){
                if(list1[i] == list2[j]){
                    answer.add(list1[i]);
                }
            }
        }

        Collections.sort(answer);

        return answer;
    }
}
```

- 풀이

간단하게 이중 for 문 돌려서 Collections 썼지만,, Time Limit Exceeded 나면서 오류발생,,

1. 예시2

```java
package Main;

import java.util.*;
/*
* 입력 예시 :
4 3
3 4 1 2
4 3 2 1
3 1 4 2

* 출력 예시 : 3
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num1 = scanner.nextInt();
        int [] list1 = new int[num1];
        for(int i=0; i<list1.length; i++){
            list1[i] = scanner.nextInt();
        }

        int num2 = scanner.nextInt();
        int [] list2 = new int[num2];
        for(int i=0; i<list2.length; i++){
            list2[i] = scanner.nextInt();
        }

        for(int x : solution(num1, num2, list1, list2)){
            System.out.print(x + " ");
        }

    }

    public static ArrayList<Integer> solution(int num1, int num2, int[] list1, int[] list2){
        ArrayList<Integer> answer = new ArrayList<>();
        Arrays.sort(list1);
        Arrays.sort(list2);

        int p1 = 0, p2 = 0;
        while(p1 < num1 && p2 < num2){
            if(list1[p1] == list2[p2]){
                answer.add(list1[p1++]);
                p2++;
            }else if(list1[p1] < list2[p2]){
                p1++;
            }else{
                p2++;
            }
        }
        return answer;
    }
}
```

- 풀이

시그니처로 받은 list1 , list2 오름차순으로 정렬 → list1[p1] 과 list2[p2] 와 같으면 answer.add 처리 후 둘다 동시에 증감처리

 → else if list1[p1] < list[p2] 이면 작은쪽이 증감(오름차순으로 정렬해놨으니까 p1 뒤에 p2 의 값이 있을수도 있으니까)

→ 아니면 p2 증감처리 return;

---

### 3. 최대매출 (Sliding Window) → O(n2) 이중포문 말구 O(n) 으로

- 설명

현수의 아빠는 제과점을 운영합니다. 현수 아빠는 현수에게 N일 동안의 매출기록을 주고 연속된 K일 동안의 최대 매출액이 얼마인지 구하라고 했습니다.

만약 N=10이고 10일 간의 매출기록이 아래와 같습니다. 이때 K=3이면

12 1511 20 2510 20 19 13 15

연속된 3일간의 최대 매출액은 11+20+25=56만원입니다.

여러분이 현수를 도와주세요.

- 입력

첫 줄에 N(5<=N<=100,000)과 K(2<=K<=N)가 주어집니다.

두 번째 줄에 N개의 숫자열이 주어집니다. 각 숫자는 500이하의 음이 아닌 정수입니다.

- 출력

첫 줄에 최대 매출액을 출력합니다.

```java
package Main;

import java.util.*;
/*
* 입력 예시 :
10 3
12 15 11 20 25 10 20 19 13 15

* 출력 예시 : 56
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num1 = scanner.nextInt();
        int num2 = scanner.nextInt();
        int [] list = new int[num1];

        for(int i=0; i<list.length; i++){
            list[i] = scanner.nextInt();
        }

        System.out.println(solution(num1, num2, list));
    }

    public static int solution(int num1, int num2, int[] list){
        int answer=0;
        int sum=0;

        for(int i=0; i<num2; i++){
            sum += list[i];
            answer = sum;
        }

        for(int i=num2; i<num1; i++){
            sum+= list[i];
            sum-= list[i-num2];
            answer = Math.max(answer, sum);
        }
        return answer;
    }
}
```

- 풀이
    
    시그니처로 받은 list 를 list[0] ~ list[2] 지점까지 sum 으로 합산. answer 에 대입 →
    
    밑에 for 문에서 i = num2(3) 대입 10 까지 돌린다 →
    
    sum 에 3부터 합산 더해주고→ 다시 sum 에 list[3 - 3] ⇒ list[0] 값을 빼준다. → 다음 for 문에서는 list [ 4 -3 ] ⇒ list[1] 이 작동→
    
    슬라이딩 형식으로 합산하고 빼준후 → return;
    

---

### 4. 연속 부분수열 → 이중 포문은 O(n2) 이여서 X → O(n) 으로 구현해야 맞음(투포인트 알고리즘 , 슬라이딩 윈도우 알고리즘)

- 설명

N개의 수로 이루어진 수열이 주어집니다.

이 수열에서 연속부분수열의 합이 특정숫자 M이 되는 경우가 몇 번 있는지 구하는 프로그램을 작성하세요.

만약 N=8, M=6이고 수열이 다음과 같다면

1 2 1 3 1 1 1 2

합이 6이 되는 연속부분수열은 {2, 1, 3}, {1, 3, 1, 1}, {3, 1, 1, 1}로 총 3가지입니다.

- 입력

첫째 줄에 N(1≤N≤100,000), M(1≤M≤100,000,000)이 주어진다.

수열의 원소값은 1,000을 넘지 않는 자연수이다.

- 출력

첫째 줄에 경우의 수를 출력한다.

```java
package Main;

import java.util.*;
/*
* 입력 예시 :
8 6
1 2 1 3 1 1 1 2

* 출력 예시 : 3
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num1 = scanner.nextInt();
        int num2 = scanner.nextInt();
        int [] arr = new int[num1];

        for(int i=0; i<arr.length; i++){
            arr[i] = scanner.nextInt();
        }

        System.out.println(solution(num1, num2, arr));
    }

    public static int solution(int num1, int num2, int[] arr){
        int answer=0;
        int sum=0, lt=0;

        for(int rt=0; rt<num1; rt++){
            sum += arr[rt]; //rt 값을 더하고 바로 확인 -> lt(0) 부터 rt 까지의 합
            if(sum == num2) answer++;
                while (sum >= num2){
                    sum -=arr[lt++]; // lt 값 뺴고 증감
                    if(sum == num2) answer++;
             }
          }
        return answer;
    }
}
```

- 풀이
    
    lt rt 가 가르키는값 설정 → arr[rt] 를 통해 sum 에 중첩으로 더해줌 → sum 이 num2 와 같으면 anwer ++ → sum 이 while 문 타고 num2 보다 같거나 클시 arr[lt++] 부분 빼주면서 증감 → sum == num2 이면 answer++ → return;
    
    이중포문 O(n2) 으로 푸는것보다 O(n) 으로 풀어야 통과
    

---

### 5. 연속된 자연수의 합(**Two pointers**)

- 설명

N입력으로 양의 정수 N이 입력되면 2개 이상의 연속된 자연수의 합으로 정수 N을 표현하는 방법의 가짓수를 출력하는 프로그램을 작성하세요.

만약 N=15이면

7+8=15

4+5+6=15

1+2+3+4+5=15

와 같이 총 3가지의 경우가 존재한다.

- 입력

첫 번째 줄에 양의 정수 N(7<=N<1000)이 주어집니다.

- 출력

첫 줄에 총 경우수를 출력합니다.

1. 예시1(내풀이)

```java
package Main;

import java.util.*;
/*
* 입력 예시 :
15

* 출력 예시 : 3
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();

        System.out.println(solution(num));
    }

    public static int solution(int num){
        int answer = 0 , sum =0 , a = 1;
        int m = num / 2 + 1; // 15는 7 + 8 이므로 8까지만 있으면 됨
        int [] arr = new int[num];

        for(int i=0; i<arr.length; i++){
            arr[i] = a;
            a++;
        }

        int lt = 0;
        for(int rt= 0; rt<m; rt++){
            sum += arr[rt];
            if(sum == num) answer++;

            while (sum >= num){
                sum -= arr[lt++];
                if(sum == num) answer++;
            }
        }

        return answer;
    }
}
```

---

### 6. 최대 길이 연속부분 수열

- 설명

0과 1로 구성된 길이가 N인 수열이 주어집니다. 여러분은 이 수열에서 최대 k번을 0을 1로 변경할 수 있습니다. 여러분이 최대 k번의 변경을 통해 이 수열에서 1로만 구성된 최대 길이의 연속부분수열을 찾는 프로그램을 작성하세요.

만약 길이가 길이가 14인 다음과 같은 수열이 주어지고 k=2라면

1 1 0 0 1 1 0 1 1 0 1 1 0 1

여러분이 만들 수 있는 1이 연속된 연속부분수열은

![https://cote.inflearn.com/public/upload/19123bb35c.jpg](https://cote.inflearn.com/public/upload/19123bb35c.jpg)

이며 그 길이는 8입니다.

- 입력

첫 번째 줄에 수열의 길이인 자연수 N(5<=N<100,000)이 주어집니다.

두 번째 줄에 N길이의 0과 1로 구성된 수열이 주어집니다.

- 출력

첫 줄에 최대 길이를 출력하세요.

```java
package Main;

import java.util.*;
/*
* 입력 예시 :
14 2
1 1 0 0 1 1 0 1 1 0 1 1 0 1

* 출력 예시 : 8
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();
        int num2 = scanner.nextInt();
        int [] arr = new int[num];

        for(int i=0; i<arr.length; i++){
            arr[i] = scanner.nextInt();
        }

        System.out.println(solution(num, num2, arr));
    }

    public static int solution(int n, int k, int [] arr){
        int answer = 0;

        int lt = 0;
        int cnt = 0; // 0 를 1로 바꾼 횟수

        for(int rt=0 ;rt<n; rt++){
            if(arr[rt] == 0 ) cnt++;
            while(cnt > k){
                if(arr[lt] == 0) cnt--;
                lt++;
            }
            answer = Math.max(answer, rt - lt + 1); // 연속 최대수열의 길이
        }
        return answer;
    }
}
```

- 풀이

rt 가 0 을 만나면 cnt ++ 증가(1로 바꿨다고 생각) → 최대수열 길이 answer 에 저장 → while 문은 cnt 가 k 초과시 조정 해줘야함 → cnt - - 후에 lt ++ 처리(0 를 1로 바꾼 횟수를 차감) 최대 수열길이는 반영 X→ → return;

---
