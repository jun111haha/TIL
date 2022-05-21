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

설명

철수는 학교에 가는데 개울을 만났습니다. 개울은 N개의 돌로 다리를 만들어 놓았습니다.

철수는 돌 다리를 건널 때 한 번에 한 칸 또는 두 칸씩 건너뛰면서 돌다리를 건널 수 있습니다.

철수가 개울을 건너는 방법은 몇 가지일까요?

![https://cote.inflearn.com/public/upload/d7efa0719e.jpg](https://cote.inflearn.com/public/upload/d7efa0719e.jpg)

입력

첫째 줄은 돌의 개수인 자연수 N(3≤N≤35)이 주어집니다.

출력

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
