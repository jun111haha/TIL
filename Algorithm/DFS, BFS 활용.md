## **1. 합이 같은 부분집합(DFS : 아마존 인터뷰)**

- 설명

N개의 원소로 구성된 자연수 집합이 주어지면, 이 집합을 두 개의 부분집합으로 나누었을 때

두 부분집합의 원소의 합이 서로 같은 경우가 존재하면 “YES"를 출력하고, 그렇지 않으면 ”NO"를 출력하는 프로그램을 작성하세요.

둘로 나뉘는 두 부분집합은 서로소 집합이며, 두 부분집합을 합하면 입력으로 주어진 원래의 집합이 되어 합니다.

예를 들어 {1, 3, 5, 6, 7, 10}이 입력되면 {1, 3, 5, 7} = {6, 10} 으로 두 부분집합의 합이 16으로 같은 경우가 존재하는 것을 알 수 있다.

- 입력

첫 번째 줄에 자연수 N(1<=N<=10)이 주어집니다.

두 번째 줄에 집합의 원소 N개가 주어진다. 각 원소는 중복되지 않는다.

- 출력

첫 번째 줄에 “YES" 또는 ”NO"를 출력한다.

```java
package Main;

import java.util.*;
/*
* 입력 예시
6
1 3 5 6 7 10
* 출력예시
YES
* */

class Main {
    static String answer = "NO";
    static int n, total = 0;
    static boolean flag = false;

    public static void DFS(int L , int sum, int[] arr ){
        if(flag) return;
        if(sum > total/ 2) return;
        if(L==n){
            if((total - sum) == sum) {
                answer = "YES";
                flag = true;
            }
        }else{
            DFS(L+1, sum + arr[L], arr);
            DFS(L+1, sum, arr);
        }
    }

    public static void main(String[] args){
        Scanner scanner = new Scanner(System.in);
        n = scanner.nextInt();
        int [] arr = new int[n];
        for(int i=0; i<n; i++){
            arr[i] = scanner.nextInt();
            total += arr[i];
        }

        DFS(0, 0, arr);
        System.out.println(answer);
    }
}
```

- 풀이
    
    

## **2. 바둑이 승차(DFS)**

- 설명

철수는 그의 바둑이들을 데리고 시장에 가려고 한다. 그런데 그의 트럭은 C킬로그램 넘게 태울수가 없다.

철수는 C를 넘지 않으면서 그의 바둑이들을 가장 무겁게 태우고 싶다.

N마리의 바둑이와 각 바둑이의 무게 W가 주어지면, 철수가 트럭에 태울 수 있는 가장 무거운 무게를 구하는 프로그램을 작성하세요.

- 입력

첫 번째 줄에 자연수 C(1<=C<=100,000,000)와 N(1<=N<=30)이 주어집니다.

둘째 줄부터 N마리 바둑이의 무게가 주어진다.

- 출력

첫 번째 줄에 가장 무거운 무게를 출력한다.

```java
package Main;

import java.util.*;
/*
* 입력 예시
259 5
81
58
42
33
61

* 출력예시
242

* */

class Main {
    static int[] arr;
    static int c, n;
    static int answer = -1;

    public static void DFS(int L , int sum){
        if(sum > c) return;
        if(L== n){
            answer= Math.max(answer, sum);
        }else{
            DFS(L+ 1, sum+ arr[L]);
            DFS(L+ 1, sum);
        }

    }

    public static void main(String[] args){
        Scanner scanner = new Scanner(System.in);
        c = scanner.nextInt();
        n = scanner.nextInt();

        arr = new int[n];
        for(int i=0; i<n; i++){
            arr[i] = scanner.nextInt();
        }

        DFS(0, 0);

        System.out.println(answer);
    }
}
```

## **3. 최대점수 구하기(DFS)**

- 설명

이번 정보올림피아드대회에서 좋은 성적을 내기 위하여 현수는 선생님이 주신 N개의 문제를 풀려고 합니다.

각 문제는 그것을 풀었을 때 얻는 점수와 푸는데 걸리는 시간이 주어지게 됩니다.

제한시간 M안에 N개의 문제 중 최대점수를 얻을 수 있도록 해야 합니다.

(해당문제는 해당시간이 걸리면 푸는 걸로 간주한다, 한 유형당 한개만 풀 수 있습니다.)

- 입력

첫 번째 줄에 문제의 개수N(1<=N<=20)과 제한 시간 M(10<=M<=300)이 주어집니다.

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
41

* */

class Main {
    static int n, m;
    static int answer = Integer.MIN_VALUE;

    public static void DFS(int L, int scoreSum, int timeSum, int[] score, int[] time){
        if(m < timeSum) return;
        if(L==n){
            answer = Math.max(answer, scoreSum);
        }else{
            DFS(L+1, scoreSum+score[L], timeSum+time[L], score, time);
            DFS(L+1, scoreSum, timeSum, score, time);
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        n = scanner.nextInt();
        m = scanner.nextInt();

        int[] score = new int[n];
        int[] time = new int[n];

        for(int i=0; i<n; i++){
            score[i] = scanner.nextInt();
            time[i] = scanner.nextInt();
        }
        DFS(0, 0, 0, score, time);
        System.out.println(answer);
    }

}
```

## 4. 중복순열

```java
package Main;

import java.util.*;
/*
* 입력 예시
3 2

* 출력예시

* */

class Main {
    static int[] pm;
    static int n, m;

    public static void DFS(int L){
        if (L == m) {
            for(int x : pm){
                System.out.print(x+ " ");
                System.out.println();
            }

        }else{
            for(int i=1; i<=n; i++){
                pm[L] = i;
                DFS(L+ i);
            }
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        n = scanner.nextInt();
        m = scanner.nextInt();

        pm = new int[m];
        DFS(0);
    }

}
```

## **5. 동전교환**

- 설명

다음과 같이 여러 단위의 동전들이 주어져 있을때 거스름돈을 가장 적은 수의 동전으로 교환해주려면 어떻게 주면 되는가?

각 단위의 동전은 무한정 쓸 수 있다.

- 입력

첫 번째 줄에는 동전의 종류개수 N(1<=N<=12)이 주어진다. 두 번째 줄에는 N개의 동전의 종류가 주어지고,

그 다음줄에 거슬러 줄 금액 M(1<=M<=500)이 주어진다.각 동전의 종류는 100원을 넘지 않는다.

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
3

* */

class Main {
    static int n, m;
    static int answer = Integer.MAX_VALUE;

    public static void DFS(int L, int sum, Integer[] arr){
        //L: 동전의 개수
        //sum: L개 동전 금액의 총합
        if(sum> m) return; //무한 안돌려면 이게 필요
        if(L>= answer) return;  //굳이 더 레벨탐색할 필요없음. 레벨 5에서 멈춤
        if(sum== m){
            answer= Math.min(answer, L);
        }else{
           for(int i=0; i<n; i++){
               DFS(L+1, sum+arr[i], arr);
           }
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        n = scanner.nextInt(); //동전 종류 개수

        Integer[] arr = new Integer[n];
        for(int i=0; i<n; i++){
            arr[i] = scanner.nextInt();
        }

        Arrays.sort(arr, Collections.reverseOrder());
        m = scanner.nextInt(); //거슬러줄 금액
        DFS(0,0, arr);
        System.out.println(answer);
    }
}
```

- 풀이
    1. 입력받은 동전들을 역순으로 정렬하여 재귀함수를 호출하게 만든다. (내림차순)
    - 오름차순으로 진행할 경우 time limit exceeded 발생
    - 내림차순으로 큰 동전부터 처리해야 시간복잡도가 많이 줄어든다
    
    예를들어 위의 예시 입력 기준으로 오름차순 진행할 경우 거스름돈이 15, 동전의 종류 1부터 시작하여 처음부터
    
    level15 까지 재귀함수를 호출하여 (백 트래킹 -> 함수호출) 반복으로 진행 되지만
    
    내림차순으로 진행할 경우 거스름돈이 15, 동전의 종류 5부터 시작하여 level3 에서 거스름값을 만들게 되고 그 이상의 level은 조건에서 return하면 불필요한 재귀함수를 호출하지 않고 시간복잡도를 대폭 줄일 수 있다.
    
    **여기서 level은 동전의 갯수로 생각한다
    
    1. Collections.reverseOrder 사용하기 위해서는 정렬하고자 하는 배열이 int이 아닌 Integer으로 선언해줘야한다.
    

## 6. 순열구하기

```java
package Main;

import java.util.*;
/*
* 입력 예시
3 2
3 6 9

* 출력예시
* */

class Main {
    static int[] pm, ch ,arr;
    static int n, m;

    public static void DFS(int L){
        if(L== m){
            for(int x : pm){
                System.out.print(x+ " ");
            }
            System.out.println();
        }else{
            for(int i=0; i<n; i++){
                if(ch[i] == 0){
                    ch[i] = 1; //사용했음 1로 체크
                    pm[L] = arr[i];
                    DFS(L+ 1);
                    ch[i] = 0; //체크해제
                }
            }
        }

    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        n = scanner.nextInt();
        m = scanner.nextInt();

        arr = new int[n];

        for(int i=0; i<n; i++){
            arr[i] = scanner.nextInt();
        }

        ch = new int[n]; //체크용 배열
        pm = new int[m]; //담는배열 배열

        DFS(0);
    }
}
```

## **7. 조합의 경우수(메모이제이션)**

- 설명

![https://cote.inflearn.com/public/upload/8f99ebbe8d.jpg](https://cote.inflearn.com/public/upload/8f99ebbe8d.jpg)

로 계산합니다.

하지만 여러분은 이 공식을 쓰지않고 다음 공식을 사용하여 재귀를 이용해 조합수를 구해주는 프로그램을 작성하세요.

![https://cote.inflearn.com/public/upload/b4a8e9f795.jpg](https://cote.inflearn.com/public/upload/b4a8e9f795.jpg)

- 입력

첫째 줄에 자연수 n(3<=n<=33)과 r(0<=r<=n)이 입력됩니다.

- 출력

첫째 줄에 조합수를 출력합니다.

```java
package Main;

import java.util.*;
/*
* 입력 예시
* 33 19

* 출력예시
* 818809200
* */

class Main {
    // 메모이제이션 할 배열 선언
    // static인 main()에서는 접근 할 필요 없고 DFS()에서만 접근하면 되니까 static으로 선언 할 필요없음
    // n의 범위가 3<=n<=33, r의 범위가 0<=r<=n이므로 넉넉히 35로 잡는다.
    static int [][] dy = new int[35][35];
    public static int DFS(int n, int r){
        //미리 구한값이 있으면 그냥 return 굳이 재귀호출 ㄴㄴ
        if(dy[n][r] >0) return dy[n][r];

        // n == r ex. 2C2인 경우, 2개 중 2개를 뽑는 경우의 수는 1
        // r == 0 ex. 2C0인 경우, 2개 중 0개를 뽑는 경우의 수는 1
        if(n == r || r == 0){
            return 1;
        }else{
            //이미 구한값 기록
            return dy[n][r] = DFS(n - 1, r - 1) + DFS(n - 1 ,r);
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int r = scanner.nextInt();

        System.out.println(DFS(n, r));
    }
}
```

## **8. 수열 추측하기**

설명

가장 윗줄에 1부터 N까지의 숫자가 한 개씩 적혀 있다. 그리고 둘째 줄부터 차례대로 파스칼의 삼각형처럼 위의 두개를 더한 값이 저장되게 된다.

예를 들어 N이 4 이고 가장 윗 줄에 3 1 2 4 가 있다고 했을 때, 다음과 같은 삼각형이 그려진다.

![https://cote.inflearn.com/public/upload/e2f3cae26a.jpg](https://cote.inflearn.com/public/upload/e2f3cae26a.jpg)

N과 가장 밑에 있는 숫자가 주어져 있을 때 가장 윗줄에 있는 숫자를 구하는 프로그램을 작성하시오.

단, 답이 여러가지가 나오는 경우에는 사전순으로 가장 앞에 오는 것을 출력하여야 한다.

입력

첫째 줄에 두개의 정수 N(1≤N≤10)과 F가 주어진다.

N은 가장 윗줄에 있는 숫자의 개수를 의미하며 F는 가장 밑에 줄에 있는 수로 1,000,000 이하이다.

출력

첫째 줄에 삼각형에서 가장 위에 들어갈 N개의 숫자를 빈 칸을 사이에 두고 출력한다.

답이 존재하지 않는 경우는 입력으로 주어지지 않는다.

```java
package Main;

import java.util.*;

class Main{
	// b : combi 값 저장
	// p : 순열 저장
	// ch : 중복되지 않는 순열이므로 ch 필요 
	static int[] b, p, ch;
	static int n, f;
	static boolean flag = false;
	int[][] dy = new int[35][35];
	public int combi(int n, int r){
		if(dy[n][r]>0) return dy[n][r];
 		if(n == r || r == 0) return 1;
		else return dy[n][r] = combi(n-1, r-1) + combi(n-1, r);
	}
	
	public void DFS(int L, int sum){
		if(flag) return;
		// (n개 중에서) n개를 뽑은 순열 하나 완성 
		if(L == n){
			if(sum==f){
				for(int x : p) System.out.print(x+" ");
								// 답을 찾았으니까 
                // 앞으로의 재귀를 모두 멈춘다 
                // (이미 쌓여있던 스택으로 복귀해서 호출한 재귀를 바로 리턴) 
                // 복귀해서 호출한 재귀 분 외에는 새롭게 뻗지 않음
				flag = true;
			}
		}
		else{
			// i는 순열의 원소 자체이므로 1~n까지("가장 윗줄에 1부터 N까지의 숫자가~") 돌아야함
			for(int i=1; i<=n; i++){
				if(ch[i]==0){
					ch[i] = 1;
					// i는 순열의 원소 자체이다.
					p[L] = i;
					DFS(L+1, sum+(p[L]*b[L]));
					ch[i]=0;
				}
			}
		}
	}	
	public static void main(String[] args){
		Main T = new Main();
		Scanner kb = new Scanner(System.in);
		n = kb.nextInt(); 
		f = kb.nextInt(); 
		b = new int[n]; 
		p = new int[n];
		// "가장 윗줄에 1부터 N까지의 숫자가~" : for문의 i가 1부터 시작하므로 ch도 1부터 시작
		ch = new int[n+1];
		
		// b 배열에는 3C0, 3C1, 3C2, 3C3값이 저장된다.
		for(int i=0; i<n; i++){
			b[i] = T.combi(n-1, i);
		}
		T.DFS(0, 0);
	}
}

```

## 전략

- (n개 중 n개를 뽑는) 중복 아닌 순열 중 16을 만들 수 있는 순열을 찾으면 됨
- 직접 시뮬레이션 할 필요없이 공식 이용> 미리 조합수(combi) 값을 구해놓은 다음 순열의 각 원소와 곱하고, 해당 각 값을 모두 더한 값이 16이 되어야한다.
- 중복되지 않아야하므로 ch배열 필요

## 9. 조합 구하기(채점지원안됨)

```java
package Main;

import java.util.*;
/*
* 입력 예시
* 4 2

* 출력예시
*
* */

class Main {

    static int n , m;
    static int [] combi;
    public static void DFS(int L, int s){
        if(L == m){
            for(int x : combi){
                System.out.print(x + " ");
            }
            System.out.println();
        }else{
            for(int i=s; i<=n; i++){
                combi[L] = i;
                DFS(L+1, i+1);
            }
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        n = scanner.nextInt();
        m = scanner.nextInt();

        combi = new int[m];
        DFS(0, 1);
    }
}
```

## **10. 미로탐색(DFS)**

- 설명

7*7 격자판 미로를 탈출하는 경로의 가지수를 출력하는 프로그램을 작성하세요.

출발점은 격자의 (1, 1) 좌표이고, 탈출 도착점은 (7, 7)좌표이다. 격자판의 1은 벽이고, 0은 통로이다.

격자판의 움직임은 상하좌우로만 움직인다. 미로가 다음과 같다면

![https://cote.inflearn.com/public/upload/72540f8a90.jpg](https://cote.inflearn.com/public/upload/72540f8a90.jpg)

위의 지도에서 출발점에서 도착점까지 갈 수 있는 방법의 수는 8가지이다.

- 입력

7*7 격자판의 정보가 주어집니다.

- 출력

첫 번째 줄에 경로의 가지수를 출력한다.

```java
package Main;

import java.util.*;
/*
* 입력 예시
*
0 0 0 0 0 0 0
0 1 1 1 1 1 0
0 0 0 1 0 0 0
1 1 0 1 0 1 1
1 1 0 0 0 0 1
1 1 0 1 1 0 0
1 0 0 0 0 0 0

* 출력예시
* 8
* */

class Main {

    static int [] dx = {-1, 0 , 1, 0};
    static int [] dy = {0, 1, 0, -1};
    static int [][] board;
    static int answer = 0;

    public static void DFS(int x, int y){
        //종착점
        if(x == 7 && y == 7){
            answer++;
        }else{
            //네방향 접근
            for(int i=0; i<4; i++){
                int nx = x+dx[i];
                int ny = y+dy[i];
                //좌표체크
                if(nx>=1 && nx<=7 && ny>=1 && ny<=7 && board[nx][ny] == 0){
                    //간지점
                    board[nx][ny] = 1;
                    DFS(nx, ny);
                    //통로리셋
                    board[nx][ny] = 0;
                }
            }
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        board = new int[8][8];
        for(int i=1; i<=7; i++){
            for(int j=1; j<=7; j++){
                board[i][j] = scanner.nextInt();
            }
        }

        //출발점 체크
        board[1][1] = 1;
        DFS(1, 1);
        System.out.println(answer);
    }
}
```

## **11. 미로의 최단거리 통로(BFS)**

- 설명

7*7 격자판 미로를 탈출하는 최단경로의 길이를 출력하는 프로그램을 작성하세요.

경로의 길이는 출발점에서 도착점까지 가는데 이동한 횟수를 의미한다.

출발점은 격자의 (1, 1) 좌표이고, 탈출 도착점은 (7, 7)좌표이다. 격자판의 1은 벽이고, 0은 도로이다.

격자판의 움직임은 상하좌우로만 움직인다. 미로가 다음과 같다면

![https://cote.inflearn.com/public/upload/88ff3b120f.jpg](https://cote.inflearn.com/public/upload/88ff3b120f.jpg)

위와 같은 경로가 최단 경로의 길이는 12이다.

- 입력

첫 번째 줄부터 7*7 격자의 정보가 주어집니다.

- 출력

첫 번째 줄에 최단으로 움직인 칸의 수를 출력한다. 도착할 수 없으면 -1를 출력한다.

```java
package Main;
import java.util.*;
/*
* 입력 예시
0 0 0 0 0 0 0
0 1 1 1 1 1 0
0 0 0 1 0 0 0
1 1 0 1 0 1 1
1 1 0 1 0 0 0
1 0 0 0 1 0 0
1 0 1 0 0 0 0

* 출력예시
12
* */
class Point{
    public int x, y;
    Point(int x, int y){
        this.x = x;
        this.y = y;
    }
}

class Main {
		// 이동할 네 가지 방향 정의 (상, 우, 하, 좌)
    static int [] dx = {-1, 0 , 1, 0};
    static int [] dy = {0, 1, 0, -1};
    static int [][] board, dis;
    public static void BFS(int x, int y){
        Queue<Point> Q = new LinkedList<>();
        Q.offer(new Point(x, y));
				// 출발점 방문 체크 (재방문 하지 않기 위해)
        board[x][y] = 1;
        while(!Q.isEmpty()){
            Point tmp = Q.poll();
            for(int i =0; i<4; i++){
                int nx = tmp.x + dx[i];
                int ny = tmp.y + dy[i];
                if(nx>=1 && nx<=7 && ny>=1 && ny<=7 && board[nx][ny] == 0){
										// 방문 체크 (재방문 하지 않기 위해)
                    board[nx][ny] = 1;
										//큐에 방문한곳 할당
                    Q.offer(new Point(nx, ny));
                    dis[nx][ny] = dis[tmp.x][tmp.y] + 1;
                }
            }
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        board = new int[8][8];
        dis   = new int[8][8];
        for(int i=1; i<=7; i++){
            for(int j=1; j<=7; j++){
                board[i][j] = scanner.nextInt();
            }
        }

        BFS(1,1);
				// 벽 때문에 도착점에 도달한 적 없는 경우
        if(dis[7][7] == 0){
            System.out.println(-1);
        }else{
				// 최단거리
            System.out.println(dis[7][7]);
        }
    }
}
```

## **12. 토마토(BFS 활용)**

- 설명

현수의 토마토 농장에서는 토마토를 보관하는 큰 창고를 가지고 있다.

토마토는 아래의 그림과 같이 격자 모양 상자의 칸에 하나씩 넣어서 창고에 보관한다.

![https://cote.inflearn.com/public/upload/a9d513f5a5.jpg](https://cote.inflearn.com/public/upload/a9d513f5a5.jpg)

창고에 보관되는 토마토들 중에는 잘 익은 것도 있지만, 아직 익지 않은 토마토들도 있을 수 있다. 보관 후 하루가 지나면,

익은 토마토들의 인접한 곳에 있는 익지 않은 토마토들은 익은 토마토의 영향을 받아 익게 된다.

하나의 토마토의 인접한 곳은 왼쪽, 오른쪽, 앞, 뒤 네 방향에 있는 토마토를 의미한다. 대각선 방향에 있는 토마토들에게는 영향을 주지 못하며,

토마토가 혼자 저절로 익는 경우는 없다고 가정한다. 현수는 창고에 보관된 토마토들이 며칠이 지나면 다 익게 되는지, 그 최소 일수를 알고 싶어 한다.

토마토를 창고에 보관하는 격자모양의 상자들의 크기와 익은 토마토들과 익지 않은 토마토들의 정보가 주어졌을 때,

며칠이 지나면 토마토들이 모두 익는지, 그 최소 일수를 구하는 프로그램을 작성하라. 단, 상자의 일부 칸에는 토마토가 들어있지 않을 수도 있다.

- 입력

첫 줄에는 상자의 크기를 나타내는 두 정수 M, N이 주어진다. M은 상자의 가로 칸의 수,

N 은 상자의 세로 칸의 수를 나타낸다. 단, 2 ≤ M, N ≤ 1,000 이다.

둘째 줄부터는 하나의 상자에 저장된 토마토들의 정보가 주어진다.

즉, 둘째 줄부터 N개의 줄에는 상자에 담긴 토마토의 정보가 주어진다.

하나의 줄에는 상자 가로줄에 들어있는 토마토의 상태가 M개의 정수로 주어진다.

정수 1은 익은 토마토, 정수 0은 익지 않은 토마토, 정수 -1은 토마토가 들어있지 않은 칸을 나타낸다.

- 출력

여러분은 토마토가 모두 익을 때까지의 최소 날짜를 출력해야 한다.

만약, 저장될 때부터 모든 토마토가 익어있는 상태이면 0을 출력해야 하고,

토마토가 모두 익지는 못하는 상황이면 -1을 출력해야 한다.

![https://www.notion.so/DFS-BFS-1084832c99fd48ab9c1e4bd6ea110caa#94985ae802414ef2ba381a14f2ad7bb2]

```java
package Main;

import java.util.*;

/*
* 입력 예시
6 4
0 0 -1 0 0 0
0 0 1 0 -1 0
0 0 -1 0 0 0
0 0 0 0 -1 1

* 출력예시
4
* */

class Point{
    public int x, y;
    Point(int x, int y){
        this.x=x;
        this.y=y;
    }
}
class Main {
    static int[] dx={-1, 0, 1, 0};
    static int[] dy={0, 1, 0, -1};
    static int[][] board, dis;
    static int n, m;
    static Queue<Point> Q=new LinkedList<>();

    public void BFS(){
        while(!Q.isEmpty()){
            Point tmp=Q.poll();
            //4방향
            for(int i=0; i<4; i++){
                int nx=tmp.x+dx[i];
                int ny=tmp.y+dy[i];
                if(nx>=0 && nx<n && ny>=0 && ny<m && board[nx][ny]==0){
                    //0이면 체크걸고 1 넣어주기
                    board[nx][ny]=1;
                    //큐에 좌표넣어주기.
                    Q.offer(new Point(nx, ny));
                    //토마토가 익을때까지 최소날짜
                    dis[nx][ny]=dis[tmp.x][tmp.y]+1;
                }
            }
        }
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        m=kb.nextInt();
        n=kb.nextInt();
        board=new int[n][m];
        dis=new int[n][m];
        for(int i=0; i<n; i++){
            for(int j=0; j<m; j++){
                board[i][j]=kb.nextInt();
                //익은 토마토 큐에 좌표넣기.
                if(board[i][j]==1) Q.offer(new Point(i, j));
            }
        }
        T.BFS();
        boolean flag=true;
        int answer=Integer.MIN_VALUE;
        for(int i=0; i<n; i++){
            for(int j=0; j<m; j++){
                //익지 않은 토마토 체크하여 flag false 처리 후 -1 출력
                if(board[i][j]==0) flag=false;
            }
        }

        if(flag){
            for(int i=0; i<n; i++){
                for(int j=0; j<m; j++){
                    //최소날짜 출력
                    answer=Math.max(answer, dis[i][j]);
                }
            }
            System.out.println(answer);
        }
        else System.out.println(-1);
    }
}
```

## **13. 섬나라 아일랜드(DFS / BFS)**

- 설명

N*N의 섬나라 아일랜드의 지도가 격자판의 정보로 주어집니다.

각 섬은 1로 표시되어 상하좌우와 대각선으로 연결되어 있으며, 0은 바다입니다.

섬나라 아일랜드에 몇 개의 섬이 있는지 구하는 프로그램을 작성하세요.

![https://cote.inflearn.com/public/upload/7c81fe29cd.jpg](https://cote.inflearn.com/public/upload/7c81fe29cd.jpg)

만약 위와 같다면 섬의 개수는 5개입니다.

- 입력

첫 번째 줄에 자연수 N(3<=N<=20)이 주어집니다.

두 번째 줄부터 격자판 정보가 주어진다.

- 출력

첫 번째 줄에 섬의 개수를 출력한다.

1. DFS

```java
package Main;

import java.util.*;

/*
* 입력 예시
7
1 1 0 0 0 1 0
0 1 1 0 1 1 0
0 1 0 0 0 0 0
0 0 0 1 0 1 1
1 1 0 1 1 0 0
1 0 0 0 1 0 0
1 0 1 0 1 0 0

* 출력예시
* 5
* */

class Main {
    static int n;
    static int answer = 0;
    //8방향 도는 좌표
    static int[] dx = {-1, -1, 0, 1, 1, 1, 0, -1};
    static int[] dy = {0, 1, 1, 1, 0, -1, -1, -1};

    public void DFS(int x, int y, int[][] board){
        for(int i=0; i<8; i++){
            //for 문 돌면서 8방향 체크
            int nx = x + dx[i];
            int ny = y + dy[i];
            if(nx>=0 && nx<n && ny>=0 && ny<n && board[nx][ny] == 1){
                board[nx][ny] = 0; //바다로 바꿔줌
                DFS(nx, ny, board);
            }
        }
    }

    public void solution(int[][] board){
        for(int i=0; i<n; i++){
            for(int j=0; j<n; j++){
                if(board[i][j] == 1){
                    answer++; //섬의 갯수 1증가
                    board[i][j] = 0;
                    DFS(i, j, board);
                }
            }
        }
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner scanner = new Scanner(System.in);
        n = scanner.nextInt();
        int [][] arr = new int[n][n];
        for(int i=0; i<n; i++){
            for(int j=0; j<n; j++){
                arr[i][j] = scanner.nextInt();
            }
        }
        T.solution(arr);
        System.out.println(answer);
    }
}
```

- 설명

for문 돌면서 1인 지점에서 값 0으로 바꾸어주고 answer ++ , dfs 호출

8방향에 대해서 1인지 체크 → 1일 경우 0으로 바꿔줌, dfs호출

1. BFS

```java
package Main;

import java.util.*;

/*
* 입력 예시
7
1 1 0 0 0 1 0
0 1 1 0 1 1 0
0 1 0 0 0 0 0
0 0 0 1 0 1 1
1 1 0 1 1 0 0
1 0 0 0 1 0 0
1 0 1 0 1 0 0

* 출력예시
* 5
* */

class Point{
    int x;
    int y;
    public Point(int x,int y){
        this.x = x;
        this.y = y;
    }
}

class Main {
    static int n;
    static int answer = 0;
    //8방향 도는 좌표
    static int[] dx = {-1, -1, 0, 1, 1, 1, 0, -1};
    static int[] dy = {0, 1, 1, 1, 0, -1, -1, -1};
    static int[][] board;
    static Queue<Point> queue = new LinkedList<>();

    static void BFS() {
        while(!queue.isEmpty()){
            Point point = queue.poll();
            for (int i = 0; i < 8; i++) {
                int nx = point.x + dx[i];
                int ny = point.y + dy[i];
                if (nx >= 0 && nx < n && ny >= 0 && ny < n && board[nx][ny] == 1) {
                    board[nx][ny] = 0; //간 곳으로 마크
                    queue.add(new Point(nx,ny));
                }
            }
        }
    }
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        n = in.nextInt();
        board = new int[n][n];

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                board[i][j] = in.nextInt();
            }
        }

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == 1) {
                    answer++;
                    queue.add(new Point(i,j));
                    board[i][j] = 0;
                    BFS();
                }
            }
        }

        System.out.println(answer);
    }
}
```

- 설명

for문 돌면서 1인 지점에서 0으로 바꾸어주고 answer++,queue에 좌표 add후 bfs호출(호출시 좌표값 필요x)

queue가 비어있지 않으면 하나빼서 8방향 검사

1인 곳이 있으면 0으로 바꾸고 queue에 add

## **14. 피자 배달 거리(삼성 SW역량평가 기출문제 : DFS활용)**

- 설명

N×N 크기의 도시지도가 있습니다. 도시지도는 1×1크기의 격자칸으로 이루어져 있습니다.

각 격자칸에는 0은 빈칸, 1은 집, 2는 피자집으로 표현됩니다. 각 격자칸은 좌표(행번호, 열 번호)로 표현됩니다.

행번호는 1번부터 N번까지이고, 열 번호도 1부터 N까지입니다.

도시에는 각 집마다 “피자배달거리”가 았는데 각 집의 피자배달거리는 해당 집과 도시의 존재하는

피자집들과의 거리 중 최소값을 해당 집의 “피자배달거리”라고 한다.

집과 피자집의 피자배달거리는 |x1-x2|+|y1-y2| 이다.

예를 들어, 도시의 지도가 아래와 같다면

![https://cote.inflearn.com/public/upload/15230e4e41.jpg](https://cote.inflearn.com/public/upload/15230e4e41.jpg)

(1, 2)에 있는 집과 (2, 3)에 있는 피자집과의 피자 배달 거리는 |1-2| + |2-3| = 2가 된다.

최근 도시가 불경기에 접어들어 우후죽순 생겼던 피자집들이 파산하고 있습니다.

도시 시장은 도시에 있는 피자집 중 M개만 살리고 나머지는 보조금을 주고 폐업시키려고 합니다.

시장은 살리고자 하는 피자집 M개를 선택하는 기준으로 도시의 피자배달거리가 최소가 되는 M개의 피자집을 선택하려고 합니다.

도시의 피자 배달 거리는 각 집들의 피자 배달 거리를 합한 것을 말합니다.

- 입력

첫째 줄에 N(2 ≤ N ≤ 50)과 M(1 ≤ M ≤ 12)이 주어진다.

둘째 줄부터 도시 정보가 입력된다.

- 출력

첫째 줄에 M개의 피자집이 선택되었을 때 도시의 최소 피자배달거리를 출력한다.
