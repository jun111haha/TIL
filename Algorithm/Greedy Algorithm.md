# **Greedy Algorithm**

## **1. 씨름 선수**

- 설명

현수는 씨름 감독입니다. 현수는 씨름 선수를 선발공고를 냈고, N명의 지원자가 지원을 했습니다.

현수는 각 지원자의 키와 몸무게 정보를 알고 있습니다.

현수는 씨름 선수 선발 원칙을 다음과 같이 정했습니다.

“A라는 지원자를 다른 모든 지원자와 일대일 비교해서 키와 몸무게 모두 A지원자 보다 높은(크고, 무겁다) 지원자가

존재하면 A지원자는 탈락하고, 그렇지 않으면 선발된다.”

N명의 지원자가 주어지면 위의 선발원칙으로 최대 몇 명의 선수를 선발할 수 있는지 알아내는 프로그램을 작성하세요.

- 입력

첫째 줄에 지원자의 수 N(5<=N<=30,000)이 주어집니다.

두 번째 줄부터 N명의 흰돌 능력치와 검은돌 능력치 정보가 차례로 주어집니다.

각 선수의 흰돌능력치가 모두 다르고, 검은돌 능력치도 모두 다릅니다. 능력치 값은 1,000,000이하의 자연수입니다.

- 출력

첫째 줄에 바둑 선수로 뽑히는 최대 인원을 출력하세요.

```java
package Main;

import java.util.*;

/*
* 입력 예시
5
172 67
183 65
180 70
170 72
181 60

* 출력예시
* 3
* */

class Body implements Comparable<Body>{
    int h;
    int w;
    public Body(int h, int w){
        this.h = h;
        this.w = w;
    }

    @Override
    public int compareTo(Body o) {
        return o.h - this.h;
    }
}

class Main {
    public static int solution(ArrayList<Body> arr, int n ){
        int cnt =0;
        Collections.sort(arr); //내림차순 정렬

				/*
        * 183 65
        * 180 70
        * 181 60
        * 172 67
        * 170 72
        * */

        int max = Integer.MIN_VALUE;
        //몸무게 비교 max 값 비교
        for(Body body : arr){
            if(body.w > max){
                max = body.w;
                cnt++;
            }
        }
        return cnt;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        ArrayList<Body> arr = new ArrayList<>();

        for(int i =0; i<n; i++){
            int h = scanner.nextInt();
            int w = scanner.nextInt();
            arr.add(new Body(h , w));
        }
        System.out.println(solution(arr, n));
    }
}
```

## **2. 회의실 배정**

설명

한 개의 회의실이 있는데 이를 사용하고자 하는 n개의 회의들에 대하여 회의실 사용표를 만들려고 한다.

각 회의에 대해 시작시간과 끝나는 시간이 주어져 있고, 각 회의가 겹치지 않게 하면서 회의실을 사용할 수 있는 최대수의 회의를 찾아라.

단, 회의는 한번 시작하면 중간에 중단될 수 없으며 한 회의가 끝나는 것과 동시에 다음 회의가 시작될 수 있다.

입력

첫째 줄에 회의의 수 n(1<=n<=100,000)이 주어진다. 둘째 줄부터 n+1 줄까지 각 회의의 정보가 주어지는데

이것은 공백을 사이에 두고 회의의 시작시간과 끝나는 시간이 주어진다. 회의시간은 0시부터 시작한다.

회의의 시작시간과 끝나는 시간의 조건은 (시작시간 <= 끝나는 시간)입니다.

출력

첫째 줄에 최대 사용할 수 있는 회의 수를 출력하여라.
