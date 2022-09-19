# 그리디 알고리즘
탐욕법(그리디) 알고리즘이란?
탐욕법(이하 '그리디') 알고리즘이란 현재 상황에서 가장 좋은 것(최선의 선택)을 고르는 알고리즘을 말합니다.
그리디 알고리즘은 동적 프로그래밍을 간단한 문제 해결에 사용하면 지나치게 많은 일을 한다는 것을 착안하여 고안되었습니다.

그리디 알고리즘은 현재 상황에서 가장 좋은 결과를 선택해나가는 방식입니다. 하지만 이 가장 좋은 결과는 최종적인 결과 도출에 대한 최적해를 보장해주는 것은 아닙니다

## 그리기 알고리즘 조건
그리디 알고리즘 조건
그리디 알고리즘을 사용하기 위해 필요한 조건은 2가지가 있습니다.

탐욕스러운 선택 조건
- 탐욕적인 선택은 항상 안전하다는 것이 보장되어야 합니다. 여기서 "안전하다"라는 것은 이 선택으로 인해 전체 문제의 최적해를 반드시 도출할 수 있어야 한다는 것입니다.

위에서는 그리디 알고리즘을 사용해 결과 도출 시 최적해가 무조건 나오지 않는다고 하지 않았나요??
그리디 알고리즘을 사용하면 무조건 최적해가 나오는 것은 아닙니다! 하지만 그리디 알고리즘을 사용해 푸는 문제가 나왔을 때 이 조건이 만족되는가? 를 생각해 충족되면 그리디 알고리즘을 사용하는 것입니다.
즉, 그리디 알고리즘을 사용하면 최적해가 나올 수 있는 문제이여야 합니다.

최적 부분 구조 조건
- 문제에 대한 최종 해결 방법이 부분 문제에 대해서도 또한 최적의 해결 방법이다라는 조건입니다.
이 말은 전체 문제의 안에는 여러 단계가 존재하고, 이 여러 단계 내의 하나 하나의 단계에 대해 최적해가 도출되어야 한다는 것입니다.

그리디 알고리즘에서 고려해야 하는 상황은 값들이 서로 영향을 주면 안된다는 것을 염두에 두어야 합니다. 위에서 사용한 예시를 한번 더 사용해 설명해보겠습니다!

![pasted image 0](https://user-images.githubusercontent.com/59434443/191036214-04eae9c5-e6d4-445a-91fe-f83b9aeb232a.png)
![pasted image 0 (1)](https://user-images.githubusercontent.com/59434443/191036263-69764a99-6938-40c6-9d84-ecd0a9f86c33.png)


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

- 설명

한 개의 회의실이 있는데 이를 사용하고자 하는 n개의 회의들에 대하여 회의실 사용표를 만들려고 한다.

각 회의에 대해 시작시간과 끝나는 시간이 주어져 있고, 각 회의가 겹치지 않게 하면서 회의실을 사용할 수 있는 최대수의 회의를 찾아라.

단, 회의는 한번 시작하면 중간에 중단될 수 없으며 한 회의가 끝나는 것과 동시에 다음 회의가 시작될 수 있다.

- 입력

첫째 줄에 회의의 수 n(1<=n<=100,000)이 주어진다. 둘째 줄부터 n+1 줄까지 각 회의의 정보가 주어지는데

이것은 공백을 사이에 두고 회의의 시작시간과 끝나는 시간이 주어진다. 회의시간은 0시부터 시작한다.

회의의 시작시간과 끝나는 시간의 조건은 (시작시간 <= 끝나는 시간)입니다.

- 출력

첫째 줄에 최대 사용할 수 있는 회의 수를 출력하여라.

```java
package Main;

import java.util.*;

/*
* 입력 예시
5
1 4
2 3
3 5
4 6
5 7

* 출력예시
* 3
* */

class Time implements Comparable<Time>{
    int s;
    int e;
    public Time(int s, int e){
        this.s = s;
        this.e = e;
    }

    @Override
    public int compareTo(Time o) {
        //끝나는시간이 같으면? 시작시간으로 오름차순으로 정렬 (음수)
        if(this.e == o.e){
            return this.s - o.s;
        //끝나는시간이 다르면? 끝나는시간으로 오름차순 정렬 (음수)
        }else{
            return this.e - o.e;
        }
    }
}

class Main {
    public static int solution(ArrayList<Time> arr, int n ){
        int et  = 0;
        int cnt = 0;
        Collections.sort(arr); //오름차순
        for(Time time : arr){
            //회의시작하는 시간이 끝나는시점보다 크거나 같으면?
            if(time.s >= et){
                //끝나는 시간 교체작업
                et = time.e;
                cnt++;
            }
        }
        return cnt;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        ArrayList<Time> arr = new ArrayList<>();

        for(int i =0; i<n; i++){
            int s = scanner.nextInt();
            int e = scanner.nextInt();
            arr.add(new Time(s , e));
        }

        System.out.println(solution(arr, n));
    }
}
```

## **3. 결혼식**

- 설명

현수는 다음 달에 결혼을 합니다.

현수는 결혼식 피로연을 장소를 빌려 3일간 쉬지 않고 하려고 합니다.

피로연에 참석하는 친구들 N명의 참석하는 시간정보를 현수는 친구들에게 미리 요구했습니다.

각 친구들은 자신이 몇 시에 도착해서 몇 시에 떠날 것인지 현수에게 알려주었습니다.

현수는 이 정보를 바탕으로 피로연 장소에 동시에 존재하는 최대 인원수를 구하여 그 인원을 수용할 수 있는 장소를 빌리려고 합니다. 여러분이 현수를 도와주세요.

만약 한 친구가 오는 시간 13, 가는시간 15라면 이 친구는 13시 정각에 피로연 장에 존재하는 것이고 15시 정각에는 존재하지 않는다고 가정합니다.

- 입력

첫째 줄에 피로연에 참석할 인원수 N(5<=N<=100,000)이 주어집니다.

두 번째 줄부터 N줄에 걸쳐 각 인원의 오는 시간과 가는 시간이 주어집니다.

시간은 첫날 0시를 0으로 해서 마지막날 밤 12시를 72로 하는 타임라인으로 오는 시간과 가는 시간이 음이 아닌 정수로 표현됩니다.

- 출력

첫째 줄에 피로연장에 동시에 존재하는 최대 인원을 출력하세요.

```java
package Main;

import java.util.*;

/*
* 입력 예시
5
14 18
12 15
15 20
20 30
5 14

* 출력예시
* 2
* */

class Time implements Comparable<Time>{
    public int time;
    public char state;
    public Time(int s, char e){
        this.time = s;
        this.state = e;
    }

    @Override
    public int compareTo(Time time) {
        //시간이 같으면 state 기준으로 정렬
        if(this.time == time.time){
            return this.state - time.state;
        //아니면 time 으로 기준
        }else{
            return this.time - time.time;
        }
    }
}

class Main {
    public static int solution(ArrayList<Time> arr){
        int cnt = 0;
        int answer = 0;
        Collections.sort(arr);

        for(Time time : arr){
            /*
            *   5 s
                12 s
                14 e
                14 s
                15 e
                15 s
                18 e
                20 e
                20 s
                30 e
            * */
            System.out.print(time.time + " " + time.state);
            System.out.println();
            if(time.state == 's'){
                cnt++;
            }else{
                cnt--;
            }
            answer = Math.max(answer, cnt);
        }
        return answer;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        ArrayList<Time> arr = new ArrayList<>();

        for(int i =0; i<n; i++){
            int s = scanner.nextInt();
            int e = scanner.nextInt();
            arr.add(new Time(s, 's'));
            arr.add(new Time(e, 'e'));
        }

        System.out.println(solution(arr));
    }
}
```

## **4. 최대 수입 스케쥴(PriorityQueue 응용문제)**

- 설명

현수는 유명한 강연자이다. N개이 기업에서 강연 요청을 해왔다. 각 기업은 D일 안에 와서 강연을 해 주면 M만큼의 강연료를 주기로 했다.

각 기업이 요청한 D와 M를 바탕으로 가장 많을 돈을 벌 수 있도록 강연 스케쥴을 짜야 한다.

단 강연의 특성상 현수는 하루에 하나의 기업에서만 강연을 할 수 있다.

- 입력

첫 번째 줄에 자연수 N(1<=N<=10,000)이 주어지고, 다음 N개의 줄에 M(1<=M<=10,000)과 D(1<=D<=10,000)가 차례로 주어진다.

- 출력

첫 번째 줄에 최대로 벌 수 있는 수입을 출력한다.

```java
package Main;

import java.util.*;

/*
* 입력 예시
6
50 2
20 1
40 2
60 3
30 3
30 1

* 출력예시
* 5
* */

class Lecture implements Comparable<Lecture>{
    public int money;
    public int date;
    public Lecture(int money, int date){
        this.money = money;
        this.date = date;
    }

    @Override
    public int compareTo(Lecture money) {
        if(this.money == money.money){
            return money.money - this.money;
        }else{
            return money.date - this.date;
        }
    }
}

class Main {
    public static int solution(ArrayList<Lecture> arr, int dayMax){
        int answer = 0;
        Collections.sort(arr);

        /*
        * PriorityQueue 란 우선순위 큐로써 일반적인 큐의 구조 FIFO(First In First Out)를 가지면서
        * 데이터가 들어온 순서대로 데이터가 나가는 것이 아닌 우선순위를 먼저 결정하고 그 우선순위가 높은 데이터가 먼저 나가는 자료구조이다.
        * */
        PriorityQueue<Integer> priorityQueueHighest = new PriorityQueue<>(Collections.reverseOrder());

        /*
        * 이중 for 문으로
        * dayMax = 3 이 1 될때까지 for 문 설정
        * 다음 for 문은 arr.get(i).date 에서 가져온 값보다 j 가 크면 break 처리
        * ex) arr.get(i).date 에서 가져온 date 가 2 이면 j 가 3 일때 break
        * date 기준으로 분기처리 -> else 일시 PriorityQueue offer 처리해준다.
        * */
        int i=0;
        for(int j= dayMax; j>=1; j--){
            for( ; i<arr.size(); i++){
                if(arr.get(i).date < j){
                    break;
                }else{
                    priorityQueueHighest.offer(arr.get(i).money);
                }
            }
            //answer 에 누적 합산
            if(!priorityQueueHighest.isEmpty()){
                answer += priorityQueueHighest.poll();
            }

        }
        return answer;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int max = 0;
        ArrayList<Lecture> arr = new ArrayList<Lecture>();

        for(int i =0; i<n; i++){
            int money = scanner.nextInt();
            int date = scanner.nextInt();
            arr.add(new Lecture(money, date));
            if(max < date) max = date;
        }

        System.out.println(solution(arr, max));
    }
}
```

## **6. 친구인가? (Disjoint-Set : Union&Find)**

- 설명

오늘은 새 학기 새로운 반에서 처음 시작하는 날이다. 현수네 반 학생은 N명이다. 현수는 각 학생들의 친구관계를 알고 싶다.

모든 학생은 1부터 N까지 번호가 부여되어 있고, 현수에게는 각각 두 명의 학생은 친구 관계가 번호로 표현된 숫자쌍이 주어진다.

만약 (1, 2), (2, 3), (3, 4)의 숫자쌍이 주어지면 1번 학생과 2번 학생이 친구이고, 2번 학생과 3번 학생이 친구, 3번 학생과 4번 학생이 친구이다.

그리고 1번 학생과 4번 학생은 2번과 3번을 통해서 친구관계가 된다.

학생의 친구관계를 나타내는 숫자쌍이 주어지면 특정 두 명이 친구인지를 판별하는 프로그램을 작성하세요.

두 학생이 친구이면 “YES"이고, 아니면 ”NO"를 출력한다.

- 입력

첫 번째 줄에 반 학생수인 자연수 N(1<=N<=1,000)과 숫자쌍의 개수인 M(1<=M<=3,000)이 주어지고,

다음 M개의 줄에 걸쳐 숫자쌍이 주어진다.

마지막 줄에는 두 학생이 친구인지 확인하는 숫자쌍이 주어진다.

- 출력

첫 번째 줄에 “YES"또는 "NO"를 출력한다.

```java
package Main;

import java.util.*;

/*
* 입력 예시
9 7
1 2
2 3
3 4
1 5
6 7
7 8
8 9
3 8

* 출력예시
* NO
* */

class Main {
    static int[] unf;
    public static int Find(int v){
        if(v==unf[v]){
            return v;
        }else{
            return unf[v] = Find(unf[v]);
        }
    }

    public static void Union(int a, int b){
        int fa = Find(a);
        int fb = Find(b);
        if(fa != fb) unf[fa] = fb;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int m = scanner.nextInt();
        unf = new int[n + 1];
        for(int i= 1; i<=n; i++){
            unf[i] = i;
        }
        for(int i= 1; i<=m; i++){
            int a = scanner.nextInt();
            int b = scanner.nextInt();
            Union(a, b);
        }

        int a = scanner.nextInt();
        int b = scanner.nextInt();
        int fa = Find(a);
        int fb = Find(b);
        if(fa == fb){
            System.out.println("YES");
        }else{
            System.out.println("NO");
        }

    }
}
```

## **7. 원더랜드(최소스패닝트리)**

- 설명

원더랜드에 문제가 생겼다. 원더랜드의 각 도로를 유지보수하는 재정이 바닥난 것이다.

원더랜드는 모든 도시를 서로 연결하면서 최소의 유지비용이 들도록 도로를 선택하고 나머지 도로는 폐쇄하려고 한다.

아래의 그림은 그 한 예를 설명하는 그림이다.

![https://cote.inflearn.com/public/upload/7d06ee1336.jpg](https://cote.inflearn.com/public/upload/7d06ee1336.jpg)

위의 지도는 각 도시가 1부터 9로 표현되었고, 지도의 오른쪽은 최소비용 196으로 모든 도시를 연결하는 방법을 찾아낸 것이다.

- 입력

첫째 줄에 도시의 개수 V(1≤V≤100)와 도로의 개수 E(1≤E≤1,000)가 주어진다.

다음 E개의 줄에는 각 도로에 대한 정보를 나타내는 세 정수 A, B, C가 주어진다.

이는 A번 도시와 B번 도시가 유지비용이 C인 도로로 연결되어 있다는 의미이다.

- 출력

모든 도시를 연결하면서 드는 최소비용을 출려한다.

1. 크루스칼 알고리즘(Union & Find)

```java
package Main;

import java.util.*;

/*
* 입력 예시
9 12
1 2 12
1 9 25
2 3 10
2 8 17
2 9 8
3 4 18
3 7 55
4 5 44
5 6 60
5 7 38
7 8 35
8 9 15

* 출력예시
* 196
* */

class Edge implements Comparable<Edge>{
    public int v1;
    public int v2;
    public int cost;

    Edge(int v1, int v2, int cost){
        this.v1 = v1;
        this.v2 = v2;
        this.cost = cost;
    }

    @Override
    public int compareTo(Edge ob){
        return this.cost - ob.cost;
    }
}

/*
*   그래프는 회로가 존재하며 트리는 존재하지 않는다.
*   트리 간선의 갯수 = 정점의 갯수 - 1
*   때문에 Union & Find을 사용하여 회로가 존재하지 않도록 구현해야 한다.
* */
class Main {
    static int[] unf;
    public static int Find(int v){
        if(v == unf[v]){
            return v;
        } else{
            return unf[v] = Find(unf[v]);
        }
    }

    public static void Union(int a, int b){
        int fa = Find(a);
        int fb = Find(b);

        if(fa != fb){
            unf[fa] = fb;
        }
    }

    public static void main(String[] args){
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int m = scanner.nextInt();
        unf = new int[n+1];
        ArrayList<Edge> arr = new ArrayList<>();

        for(int i=1; i<=n; i++){
            unf[i] = i;
        }

        for(int i=1; i<=m; i++){
            int a = scanner.nextInt();
            int b = scanner.nextInt();
            int c = scanner.nextInt();
            arr.add(new Edge(a, b, c));
        }

        int answer = 0;
        Collections.sort(arr);
        for(Edge ob : arr){
            int fv1 = Find(ob.v1);
            int fv2 = Find(ob.v2);
            if(fv1 != fv2){
                answer += ob.cost;
                Union(ob.v1, ob.v2);
            }
        }

        scanner.close();

        System.out.println(answer);
    }
}
```

1. 프림 : PriorityQueue

```java
package Main;

import java.util.*;

/*
* 입력 예시
9 12
1 2 12
1 9 25
2 3 10
2 8 17
2 9 8
3 4 18
3 7 55
4 5 44
5 6 60
5 7 38
7 8 35
8 9 15

* 출력예시
* 196
* */

class Edge implements Comparable<Edge>{
    public int vex;
    public int cost;

    Edge(int vex, int cost){
        this.vex  = vex;
        this.cost = cost;
    }

    @Override
    public int compareTo(Edge ob){
        return this.cost - ob.cost;
    }
}

/*
* 그래프에서 하나의 꼭짓점을 선택하여 트리를 만든다.
* 선택한 간선의 정점으로부터 가장 낮은 가중치를 갖는 정점을 선택한다.
* 모든 정점이 선택될 때까지 반복한다.
* */
class Main {
    static int[] ch;
    public static void main(String[] args){
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int m = scanner.nextInt();
        //인접리스트
        ArrayList<ArrayList<Edge>> graph = new ArrayList<ArrayList<Edge>>();

        for(int i=0; i<=n; i++){
            graph.add(new ArrayList<Edge>());
        }

        int [] ch = new int[n+1];
        for(int i=0; i<m; i++){
            int a = scanner.nextInt();
            int b = scanner.nextInt();
            int c = scanner.nextInt();
            //무방향 그래프이므로
            graph.get(a).add(new Edge(b, c));
            graph.get(b).add(new Edge(a, c));
        }

        int answer=0;
        PriorityQueue<Edge> pQ = new PriorityQueue<Edge>();
        //1번 정점부터 출발 비용은 0
        pQ.offer(new Edge(1, 0));
        while (!pQ.isEmpty()){
            Edge tmp = pQ.poll();
            int ev = tmp.vex;
            //회로가 되는것을 방지
            if(ch[ev] == 0){
                ch[ev] = 1;
                answer += tmp.cost;
                for(Edge ob : graph.get(ev)){
                    //방문안한 간선만 넣어야하는 분기처리
                    if(ch[ob.vex] == 0 ) pQ.offer(new Edge(ob.vex, ob.cost));
                }
            }
        }

        System.out.println(answer);
    }
}
```
