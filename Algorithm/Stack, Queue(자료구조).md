## **1. 올바른 괄호(Stack)**

- 설명

괄호가 입력되면 올바른 괄호이면 “YES", 올바르지 않으면 ”NO"를 출력합니다.

(())() 이것은 괄호의 쌍이 올바르게 위치하는 거지만, (()()))은 올바른 괄호가 아니다.

- 입력

첫 번째 줄에 괄호 문자열이 입력됩니다. 문자열의 최대 길이는 30이다.

- 출력

첫 번째 줄에 YES, NO를 출력한다.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
(()(()))(()

* 출력 예시 :NO
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        String str1 = scanner.next();
        System.out.println(solution(str1));
    }

    public static String solution(String str){
        String answer = "YES";
        Stack<Character> stack = new Stack<>();

        for(int i=0; i<str.length(); i++){
            if(str.charAt(i) == '('){
                stack.push(str.charAt(i));
            }else{
                if(stack.isEmpty()){
                    return "NO";
                }
                stack.pop();
            }

        }
        if(!stack.isEmpty()) return "NO";
        return answer;
    }
}
```

- 풀이

Stack 자료구조 이용해서 풀이 → 반복문 돌려서 들어갈 스택이 ‘(’ 이면 ( 애초에 ‘)’ 이면 넣지를 않음 )  stack  에 푸쉬 →

아니고 스택이 비어있으면( ’(’ 가 안들어 갔으므로) return “NO”; → 상단에 있는 stack.pop() 처리 → 여는 괄호 많음 방지로 for 다 돌고 스택이 값이 남아있으면 return “NO”;

---

## 2. 괄호문자제거

- 설명

입력된 문자열에서 소괄호 ( ) 사이에 존재하는 모든 문자를 제거하고 남은 문자만 출력하는 프로그램을 작성하세요.

- 입력

첫 줄에 문자열이 주어진다. 문자열의 길이는 100을 넘지 않는다.

- 출력

남은 문자만 출력한다.

1. 내풀이

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
(A(BC)D)EF(G(H)(IJ)K)LM(N)

* 출력 예시 : EFLM
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        String str1 = scanner.next();
        System.out.println(solution(str1));
    }

    public static String solution(String str){
        String answer = "";
        Stack<Character> stack = new Stack<>();

        for(int i=0; i<str.length(); i++){
            if(str.charAt(i) == '('){
                stack.push(str.charAt(i));
            }else if(str.charAt(i) == ')'){
                stack.pop();
            }else{
                if(stack.isEmpty()){
                    answer += str.charAt(i);
                }
            }
        }

        return answer;
    }
}
```

1. 다른 풀이

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
(A(BC)D)EF(G(H)(IJ)K)LM(N)

* 출력 예시 : EFLM
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        String str1 = scanner.next();
        System.out.println(solution(str1));
    }

    public static String solution(String str){
        String answer = "";
        Stack<Character> stack = new Stack<>();

        for(char c : str.toCharArray()){
            if(c == ')'){
                //pop 꺼낸 값을 리턴받음
                while (stack.pop() != '(');

            }else{
                stack.push(c);
            }
        }
        for(int i=0; i<stack.size(); i++) answer += stack.get(i);

        return answer;
    }
}
```

---

## 3. 크레인 인형뽑기

- 입력

첫 줄에 자연수 N(5<=N<=30)이 주어집니다.

두 번째 줄부터 N*N board 배열이 주어집니다.

board의 각 칸에는 0 이상 100 이하인 정수가 담겨있습니다.

0은 빈 칸을 나타냅니다.

1 ~ 100의 각 숫자는 각기 다른 인형의 모양을 의미하며 같은 숫자는 같은 모양의 인형을 나타냅니다.

board배열이 끝난 다음줄에 moves 배열의 길이 M이 주어집니다.

마지막 줄에는 moves 배열이 주어집니다.

moves 배열의 크기는 1 이상 1,000 이하입니다.

moves 배열 각 원소들의 값은 1 이상이며 board 배열의 가로 크기 이하인 자연수입니다.

- 출력

첫 줄에 터트려져 사라진 인형의 개수를 출력합니다.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
5
0 0 0 0 0
0 0 1 0 3
0 2 5 0 1
4 2 4 4 2
3 5 1 3 1

8
1 5 3 5 1 2 1 4

* 출력 예시 : 4
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int [][] board = new int[n][n];
        for(int i=0; i<n; i++){
            for(int j=0; j<n; j++){
                board[i][j] = scanner.nextInt();
            }
        }

        int m = scanner.nextInt();
        int [] moves = new int[m];
        for(int i=0; i<m; i++){
            moves[i] = scanner.nextInt();
        }

        System.out.println(solution(board, moves));
    }

    public static int solution(int [][] board, int [] moves){
        int answer = 0;
        Stack<Integer> stack = new Stack<>();

        for(int pos : moves){
            //board.length => 2차원 배열의 행크기 board[0].length => 열 크기
            for(int i=0; i< board.length; i++){
                if(board[i][pos-1] != 0){
                    int tmp = board[i][pos - 1];
                    board[i][pos - 1] = 0; //꺼내버린 인형 0 으로 치환
                    if(!stack.isEmpty() && tmp == stack.peek()){
                        answer +=2; //터진 인형이 2개
                        stack.pop(); //똑같은 인형 pop 처리
                    }else{
                        stack.push(tmp);
                    }
                    break; //크레인이 내려가는상황 하나꺼내면 for 문 중단.
                }
            }
        }
        return answer;
    }
}
```

- 풀이

peek() : 그냥 값만 리턴

pop() : 꺼내면서 값은 리턴 

---

## **4. 후위식 연산(postfix)**

- 설명

후위연산식이 주어지면 연산한 결과를 출력하는 프로그램을 작성하세요.

만약 3*(5+2)-9 을 후위연산식으로 표현하면 352+*9- 로 표현되며 그 결과는 12입니다.

- 입력

첫 줄에 후위연산식이 주어집니다. 연산식의 길이는 50을 넘지 않습니다.

식은 1~9의 숫자와 +, -, *, / 연산자로만 이루어진다.

- 출력

연산한 결과를 출력합니다.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
352+*9-

* 출력 예시 : 12
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        String str = scanner.next();

        System.out.println(solution(str));
    }

    public static int solution(String str){
        int answer = 0;
        Stack<Integer> stack = new Stack<>();

        for(char c : str.toCharArray()){
            //숫자인지 판별
            if(Character.isDigit(c)){
                stack.push(c - 48); //숫자로 넣기위해서
            }else{
							//rt 를 먼저 꺼냄
                int rt = stack.pop();
                int lt = stack.pop();
                if(c == '+'){
                    stack.push(rt + lt);
                }else if(c == '-'){
                    stack.push(lt - rt);
                }else if(c == '*'){
                    stack.push(lt * rt);
                }else if(c == '/'){
                    stack.push(lt / rt);
                }
            }
        }
        answer = stack.get(0);
        return answer;
    }
}
```

- 풀이

받은 시그니처를 숫자인지 판별 → 숫자이면 stack.push() → stack 에서 pop() 하여 rt 에 먼저 저장 그후 lt 도 pop 처리 →

연산자비교 하여 계산하여 다시 stack 에 push 처리 answer 에 값 저장 return

---

## 5. 쇠막대기

- 설명

여러 개의 쇠막대기를 레이저로 절단하려고 한다. 효율적인 작업을 위해서 쇠막대기를 아래에서 위로 겹쳐 놓고,

레이저를 위에서 수직으로 발사하여 쇠막대기들을 자른다. 쇠막대기와 레이저의 배치는 다음 조건을 만족한다.

- 쇠막대기는 자신보다 긴 쇠막대기 위에만 놓일 수 있다. - 쇠막대기를 다른 쇠막대기 위에 놓는 경우 완전히 포함되도록 놓되,

끝점은 겹치지 않도록 놓는다.

- 각 쇠막대기를 자르는 레이저는 적어도 하나 존재한다.
- 레이저는 어떤 쇠막대기의 양 끝점과도 겹치지 않는다.

아래 그림은 위 조건을 만족하는 예를 보여준다. 수평으로 그려진 굵은 실선은 쇠막대기이고, 점은 레이저의 위치,

수직으로 그려진 점선 화살표는 레이저의 발사 방향이다.

![https://cote.inflearn.com/public/upload/35b4910834.jpg](https://cote.inflearn.com/public/upload/35b4910834.jpg)

이러한 레이저와 쇠막대기의 배치는 다음과 같이 괄호를 이용하여 왼쪽부터 순서대로 표현할 수 있다.

1. 레이저는 여는 괄호와 닫는 괄호의 인접한 쌍 ‘( ) ’ 으로 표현된다. 또한, 모든 ‘( ) ’는 반 드시 레이저를 표현한다.

2. 쇠막대기의 왼쪽 끝은 여는 괄호 ‘ ( ’ 로, 오른쪽 끝은 닫힌 괄호 ‘) ’ 로 표현된다.

위 예의 괄호 표현은 그림 위에 주어져 있다.

쇠막대기는 레이저에 의해 몇 개의 조각으로 잘려지는데, 위 예에서 가장 위에 있는 두 개의 쇠막대기는 각각 3개와 2개의 조각으로 잘려지고,

이와 같은 방식으로 주어진 쇠막대기들은 총 17개의 조각으로 잘려진다.

쇠막대기와 레이저의 배치를 나타내는 괄호 표현이 주어졌을 때, 잘려진 쇠막대기 조각의 총 개수를 구하는 프로그램을 작성하시오.

- 입력

한 줄에 쇠막대기와 레이저의 배치를 나타내는 괄호 표현이 공백없이 주어진다. 괄호 문자의 개수는 최대 100,000이다.

- 출력

잘려진 조각의 총 개수를 나타내는 정수를 한 줄에 출력한다.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
()(((()())(())()))(())

* 출력 예시 : 17
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        String str = scanner.next();

        System.out.println(solution(str));
    }

    public static int solution(String str){
        int answer = 0;
        Stack<Character> stack = new Stack<>();

        for(int i=0; i<str.length(); i++){
            if(str.charAt(i) == '('){
                stack.push('(');
            }else{
                stack.pop();
                if(str.charAt(i - 1) =='('){ //레이저 지점
                    answer += stack.size(); //스택에 있는 막대기갯수 누적처리
                }else{
                    answer++; //잘려나간 막대기 +1 처리
                }
            }

        }
        return answer;
    }
}
```

- 풀이

‘(’ 만나면 stack 에 ‘(’ 을 push 한다 →  ‘)’ 를 만났을경우에는 stack 에서 pop 처리한다. → 만약 ‘)’ 의 전 문자가 ‘(’ 이였다면 레이저를 의미 → stack 사이즈만큼 더해준다. → 만약 ')' 바로 전 문자가 ')'이었다면, 그것은 단순히 닫힌 문자열이므로 answer에 +1을 한다.(단순한 닫힌 괄호는 하나의 막대 조각을 가리키게 됩니다.)→ return;

---

## **6. 공주 구하기(큐)**

- 설명

정보 왕국의 이웃 나라 외동딸 공주가 숲속의 괴물에게 잡혀갔습니다.

정보 왕국에는 왕자가 N명이 있는데 서로 공주를 구하러 가겠다고 합니다.

정보왕국의 왕은 다음과 같은 방법으로 공주를 구하러 갈 왕자를 결정하기로 했습니다.

왕은 왕자들을 나이 순으로 1번부터 N번까지 차례로 번호를 매긴다.

그리고 1번 왕자부터 N번 왕자까지 순서대로 시계 방향으로 돌아가며 동그랗게 앉게 한다.

그리고 1번 왕자부터 시계방향으로 돌아가며 1부터 시작하여 번호를 외치게 한다.

한 왕자가 K(특정숫자)를 외치면 그 왕자는 공주를 구하러 가는데서 제외되고 원 밖으로 나오게 된다.

그리고 다음 왕자부터 다시 1부터 시작하여 번호를 외친다.

이렇게 해서 마지막까지 남은 왕자가 공주를 구하러 갈 수 있다.

![https://cote.inflearn.com/public/upload/c0b0b7a761.jpg](https://cote.inflearn.com/public/upload/c0b0b7a761.jpg)

예를 들어 총 8명의 왕자가 있고, 3을 외친 왕자가 제외된다고 하자. 처음에는 3번 왕자가 3을 외쳐 제외된다.

이어 6, 1, 5, 2, 8, 4번 왕자가 차례대로 제외되고 마지막까지 남게 된 7번 왕자에게 공주를 구하러갑니다.

N과 K가 주어질 때 공주를 구하러 갈 왕자의 번호를 출력하는 프로그램을 작성하시오.

- 입력

첫 줄에 자연수 N(5<=N<=1,000)과 K(2<=K<=9)가 주어진다.

- 출력

첫 줄에 마지막 남은 왕자의 번호를 출력합니다.

1. 풀이1

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
8 3

* 출력 예시 : 7
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int m = scanner.nextInt();

        System.out.println(solution(n,m));
    }

    public static int solution(int n, int m){
        int answer = 0;
        List<Integer> list = new ArrayList<>();

        for(int i=0; i<n; i++){
            list.add(i + 1);
        }

        int removeLocation = 0;
        int beforeLocation = 0;
        while (list.size() != 1){
            //삭제할 위치 계산
            removeLocation = (beforeLocation + m) % list.size();
            //이전 삭제 위치 기억
            beforeLocation = removeLocation - 1;
            if(beforeLocation < 0){
                beforeLocation = list.size() - 1;
            }
            list.remove(beforeLocation);
        }
        answer = list.get(0);
        return answer;
    }
}
```

1. 풀이2(큐 이용)

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
8 3

* 출력 예시 : 7
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int m = scanner.nextInt();

        System.out.println(solution(n,m));
    }

    public static int solution(int n, int m){
        int answer = 0;

        //큐선언
        Queue<Integer> queue = new LinkedList<>();
        for(int i=1; i<=n; i++){
            queue.offer(i); //큐에 넣는방법
        }

        while (!queue.isEmpty()){
            for(int i=1; i<m; i++){
                //poll => 큐에서 자료를 꺼내서 리턴
                queue.offer(queue.poll()); // 1 2 3 4 5 6 7 8  -> 4 5 6 7 8 9 1 2 처리
            }
            queue.poll(); // 3꺼내고 6꺼내고..
            if(queue.size() == 1) answer = queue.poll();
        }

        return answer;
    }
}
```

---

## **7. 교육과정 설계(큐)**

- 설명

현수는 1년 과정의 수업계획을 짜야 합니다.

수업중에는 필수과목이 있습니다. 이 필수과목은 반드시 이수해야 하며, 그 순서도 정해져 있습니다.

만약 총 과목이 A, B, C, D, E, F, G가 있고, 여기서 필수과목이 CBA로 주어지면 필수과목은 C, B, A과목이며 이 순서대로 꼭 수업계획을 짜야 합니다.

여기서 순서란 B과목은 C과목을 이수한 후에 들어야 하고, A과목은 C와 B를 이수한 후에 들어야 한다는 것입니다.

현수가 C, B, D, A, G, E로 수업계획을 짜면 제대로 된 설계이지만

C, G, E, A, D, B 순서로 짰다면 잘 못 설계된 수업계획이 됩니다.

수업계획은 그 순서대로 앞에 수업이 이수되면 다음 수업을 시작하다는 것으로 해석합니다.

수업계획서상의 각 과목은 무조건 이수된다고 가정합니다.

필수과목순서가 주어지면 현수가 짠 N개의 수업설계가 잘된 것이면 “YES", 잘못된 것이면 ”NO“를 출력하는 프로그램을 작성하세요.

- 입력

첫 줄에 한 줄에 필수과목의 순서가 주어집니다. 모든 과목은 영문 대문자입니다.

두 번 째 줄부터 현수가 짠 수업설계가 주어집니다.(수업설계의 길이는 30이하이다)

- 출력

첫 줄에 수업설계가 잘된 것이면 “YES", 잘못된 것이면 ”NO“를 출력합니다.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
CBA
CBDAGE

* 출력 예시 : YES
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        String str1 = scanner.next();
        String str2 = scanner.next();

        System.out.println(solution(str1,str2));
    }

    public static String solution(String str1, String str2){
        String answer = "YES";
        Queue<Character> queue1 = new LinkedList<>();

        for(int i=0; i<str1.length(); i++){
            queue1.offer(str1.charAt(i));
        }

        for(char c : str2.toCharArray()){
            if(queue1.contains(c)){
                if(queue1.poll() != c){
                    return "NO";
                }
            }
        }
         if(!queue1.isEmpty()) answer = "NO";

       return answer;
    }
}
```

---

## **8. 응급실**

- 설명

메디컬 병원 응급실에는 의사가 한 명밖에 없습니다.

응급실은 환자가 도착한 순서대로 진료를 합니다. 하지만 위험도가 높은 환자는 빨리 응급조치를 의사가 해야 합니다.

이런 문제를 보완하기 위해 응급실은 다음과 같은 방법으로 환자의 진료순서를 정합니다.

- 환자가 접수한 순서대로의 목록에서 제일 앞에 있는 환자목록을 꺼냅니다.
- 나머지 대기 목록에서 꺼낸 환자 보다 위험도가 높은 환자가 존재하면 대기목록 제일 뒤로 다시 넣습니다. 그렇지 않으면 진료를 받습니다.

즉 대기목록에 자기 보다 위험도가 높은 환자가 없을 때 자신이 진료를 받는 구조입니다.

현재 N명의 환자가 대기목록에 있습니다.

N명의 대기목록 순서의 환자 위험도가 주어지면, 대기목록상의 M번째 환자는 몇 번째로 진료를 받는지 출력하는 프로그램을 작성하세요.

대기목록상의 M번째는 대기목록의 제일 처음 환자를 0번째로 간주하여 표현한 것입니다.

- 입력

첫 줄에 자연수 N(5<=N<=100)과 M(0<=M<N) 주어집니다.

두 번째 줄에 접수한 순서대로 환자의 위험도(50<=위험도<=100)가 주어집니다.

위험도는 값이 높을 수록 더 위험하다는 뜻입니다. 같은 값의 위험도가 존재할 수 있습니다.

- 출력

M번째 환자의 몇 번째로 진료받는지 출력하세요.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
5 2
60 50 70 80 90

* 출력 예시 : 3
* */

class Patient { // 환자 instance
    int id; // 접수 순서
    int priority; // 위험도(우선순위)

    public Patient(int id, int danger) {
        this.id = id;
        this.priority = danger;
    }
}

public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int m = scanner.nextInt();
        int [] arr = new int[n];

        for(int i=0; i<n; i++){
            arr[i] = scanner.nextInt();
        }
        System.out.println(solution(n,m,arr));
    }

    public static int solution(int n, int m, int [] arr){
        int answer = 0;
        Queue<Patient> queue = new LinkedList<>();

        for(int i=0; i<arr.length; i++){
            queue.offer(new Patient(i, arr[i])); //객체로 offer 처리 0.50, 1.60 ... 이런식으로
        }

//        System.out.println(queue.poll().id);
//        System.out.println(queue.poll().priority);

        while (!queue.isEmpty()){
            Patient temp = queue.poll(); // 객체로 temp 로 꺼내서 저장
            for(Patient x : queue){
                if(temp.priority < x.priority){ //temp.priority = 60 < x.priority = 50.. 이런식으로 비교
                    queue.offer(temp);
                    temp = null;
                    break;
                }
            }
            if(temp != null){
                answer++;
                if(temp.id == m) return answer;
            }
        }

        return answer;
    }
}
```

- 풀이

Patient 클래스 생성 객체로 관리 → queue 에서 poll 하여 temp 에 임시로 저장 → for 문을 돌려서 Patient 객체 에서 위험도를 비교 → 하나씩 비교하여 위험도가 더 높은 환자가 있으면 temp 에 null 처리 더 비교할필요 없으므로 break → 제일 큰 위험도를 만났을때 if문을 타지 않으므로 두번째 if문에서 null 확인후 없으면 answer++ 처리 → 큰 위험도는 poll() 처리 → 이런식으로 비교하여 solution 시그니처의 id 를 만날때까지 while 문을 돌린다 → 그 후에 return;

---
