## **String(문자열)**

## 1. 문자찾기

```java
package BaekJoon;

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.next();
        char c = scanner.next().charAt(0);

        System.out.println(solution(str, c));
    }

    public static int solution(String str , char t){
        int cnt = 0;
        str = str.toLowerCase();
        t = Character.toLowerCase(t);

//        for(int i=0; i<str.length(); i++){
//            if(str.charAt(i) == t){
//                cnt++;
//            }
//        }

        //문자 배열로 생성된다.
        for(char c : str.toCharArray()){
            if(c == t) cnt++;
        }

        return cnt;
    }
}
```

---

## 2. 대소문자 변환

```java
package BaekJoon;

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.next();
        System.out.println(solution(str));
    }

    public static String solution(String str) {
        String answer = "";

        for(char c : str.toCharArray()){
//            if(Character.isLowerCase(c)){
//                answer += Character.toUpperCase(c);
//            }else{
//                answer += Character.toLowerCase(c);
//            }

            /*
             * 아스키넘버 대문자 65~90
             * 아스키넘버 소문자 97~122 => 둘 차이 32
             * */
            if(c>=97 && c<=122){
                answer += (char)(c-32);
            }else{
                answer += (char)(c+32);
            }
        }
        return answer;
    }
}
```

---

## 3. 문장 속 단어

- 설명

한 개의 문장이 주어지면 그 문장 속에서 가장 긴 단어를 출력하는 프로그램을 작성하세요.

문장속의 각 단어는 공백으로 구분됩니다.

- 입력

첫 줄에 길이가 100을 넘지 않는 한 개의 문장이 주어집니다. 문장은 영어 알파벳으로만 구성되어 있습니다.

- 출력

첫 줄에 가장 긴 단어를 출력한다. 가장 길이가 긴 단어가 여러개일 경우 문장속에서 가장 앞쪽에 위치한 단어를 답으로 합니다.

1. 이렇게 풀면 런타임 오류,, 더 쉬운방식이 있을듯?

```java
package BaekJoon;

import java.util.Arrays;
import java.util.List;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.nextLine();
        System.out.println(solution(str));
    }

    public static String solution(String str) {
        String answer = "";
        List<String > list = Arrays.asList(str.split(" "));

        String str1 = list.get(0);
        for(int i=1; i<list.size(); i++){
            if(str1.length() <= list.get(i).length()){
                answer = list.get(i);
            }
        }

        return answer;
    }
}
```

1. 이렇게 풀어야 런타임 오류 해결!

```java
package BaekJoon;

import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.nextLine();
        System.out.println(solution(str));
    }

    public static String solution(String str) {
        String answer = "";
        int m = Integer.MIN_VALUE;
        String [] list = str.split(" ");

        for(String s : list){
            int len = s.length();
            if(len>m){
                m = len;
                answer = s;
            }
        }

        return answer;
    }
}
```

1. 방식2

```java
package BaekJoon;

import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.nextLine();
        System.out.println(solution(str));
    }

    public static String solution(String str) {
        String answer = "";
        int m = Integer.MIN_VALUE, pos;

        while((pos = str.indexOf(" ")) != -1){
            String tmp = str.substring(0, pos);
            int len = tmp.length();
            if(len > m){
                m=len;
                answer = tmp;
            }
            str = str.substring(pos+1);
        }
        //마지막 단어 처리
        if(str.length() > m) answer = str;
        return answer;
    }
}
```

---

## 4. 단어 뒤집기

- 설명

N개의 단어가 주어지면 각 단어를 뒤집어 출력하는 프로그램을 작성하세요.

- 입력

첫 줄에 자연수 N(3<=N<=20)이 주어집니다.

두 번째 줄부터 N개의 단어가 각 줄에 하나씩 주어집니다. 단어는 영어 알파벳으로만 구성되어 있습니다.

- 출력

N개의 단어를 입력된 순서대로 한 줄에 하나씩 뒤집어서 출력합니다.

1. 내 풀이(StringBuilder)

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        String [] str = new String[n];

        for(int i=0; i<str.length; i++){
            str[i] = scanner.next();
        }

        for(String s : solution(n, str)){
            System.out.println(s);
        }
    }

    public static ArrayList<String> solution(int n , String[] str){
        ArrayList<String> answer = new ArrayList<>();

        for(String s : str){
            String tmp = new StringBuilder(s).reverse().toString();
            answer.add(tmp);
        }
        return answer;
    }
}
```

2.StringBuilder 사용 안하고 직접 알고리즘 구현

```java

import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        String [] str = new String[n];

        for(int i=0; i<str.length; i++){
            str[i] = scanner.next();
        }

        for(String s : solution(n, str)){
            System.out.println(s);
        }
    }

    //LT RT로 char 배열에서 문자교체.
    public static ArrayList<String> solution(int n , String[] str){
        ArrayList<String> answer = new ArrayList<>();
        for(String s : str){
            char[] c = s.toCharArray();
            int lt =0;
            int rt = c.length-1;

            //문자 교체
            while(lt<rt){
                char tmp = c[lt];
                c[lt] = c[rt];
                c[rt] = tmp;
                lt++;
                rt--;
            }

            String tmp = String.valueOf(c);
            answer.add(tmp);
        }
        return answer;
    }
}
```

---

## 5. 특정 문자 뒤집기

- 설명

영어 알파벳과 특수문자로 구성된 문자열이 주어지면 영어 알파벳만 뒤집고,

특수문자는 자기 자리에 그대로 있는 문자열을 만들어 출력하는 프로그램을 작성하세요.

- 입력

첫 줄에 길이가 100을 넘지 않는 문자열이 주어집니다.

- 출

첫 줄에 알파벳만 뒤집힌 문자열을 출력합니다.

1. 예시1

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.next();
        System.out.println(solution(str));
    }

    //LT RT로 char 배열에서 문자교체.
    public static String solution(String str){
        String answer;
        char [] c = str.toCharArray();
        int lt = 0;
        int rt = c.length - 1;

        while(lt < rt){
            if(!Character.isAlphabetic(c[lt])){
                lt++;
            }else if(!Character.isAlphabetic(c[rt])){
                rt--;
            }else{
                char tmp = c[lt];
                c[lt] = c[rt];
                c[rt] = tmp;
                lt++;
                rt--;
            }
        }
        answer = String.valueOf(c);
        return answer;
    }
}
```

---

## 6. 중복문자제거

- 설명

소문자로 된 한개의 문자열이 입력되면 중복된 문자를 제거하고 출력하는 프로그램을 작성하세요.

중복이 제거된 문자열의 각 문자는 원래 문자열의 순서를 유지합니다.

- 입력

첫 줄에 문자열이 입력됩니다. 문자열의 길이는 100을 넘지 않는다.

- 출력

첫 줄에 중복문자가 제거된 문자열을 출력합니다.

1. indexof 메서드를 통해서 같은문자가 일치할시, answer 에 중첩

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.next();
        System.out.println(solution(str));
    }
    
    public static String solution(String str){
        String answer = "";

        for(int i=0; i<str.length(); i++){
            if(str.indexOf(str.charAt(i)) == i){
                answer += str.charAt(i);
            }
        }
        return answer;
    }
}
```

---

## 7. 회문 문자열

- 설명

앞에서 읽을 때나 뒤에서 읽을 때나 같은 문자열을 회문 문자열이라고 합니다.

문자열이 입력되면 해당 문자열이 회문 문자열이면 "YES", 회문 문자열이 아니면 “NO"를 출력하는 프로그램을 작성하세요.

단 회문을 검사할 때 대소문자를 구분하지 않습니다.

- 입력

첫 줄에 길이 100을 넘지 않는 공백이 없는 문자열이 주어집니다.

- 출력

첫 번째 줄에 회문 문자열인지의 결과를 YES 또는 NO로 출력합니다.

1. 예시1(내풀이)

```java
package BaekJoon;

import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.next();
        System.out.println(solution(str));
    }

    public static String solution(String str){
        String answer = "YES";
        str = str.toLowerCase();
        int len = str.length();

        for(int i=0; i < len/2; i++) {
            if (str.charAt(i) != str.charAt(len - i - 1)) return "NO";
        }
        return answer;
    }
}
```

1. 예시2

```java
package BaekJoon;

import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.next();
        System.out.println(solution(str));
    }

    public static String solution(String str){
        String answer = "NO";
        String tmp = new StringBuilder(str).reverse().toString();

        //equalsIgnoreCase 알파벳 대소문자 무시
        if(str.equalsIgnoreCase(tmp)) answer = "YES";

        return answer;
    }
}
```

---

## 8. 유효한 팰린드롬

- 설명

앞에서 읽을 때나 뒤에서 읽을 때나 같은 문자열을 팰린드롬이라고 합니다.

문자열이 입력되면 해당 문자열이 팰린드롬이면 "YES", 아니면 “NO"를 출력하는 프로그램을 작성하세요.

단 회문을 검사할 때 알파벳만 가지고 회문을 검사하며, 대소문자를 구분하지 않습니다.

알파벳 이외의 문자들의 무시합니다.

- 입력

첫 줄에 길이 100을 넘지 않는 공백이 없는 문자열이 주어집니다.

- 출력

첫 번째 줄에 팰린드롬인지의 결과를 YES 또는 NO로 출력합니다.

1. 예시(내풀이)

```java
package BaekJoon;

import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.nextLine();
        System.out.println(solution(str));
    }

    public static String solution(String str){
        String answer = "NO";
				
				//알파벳 대문자가 아니면 빈문자 처리
        str = str.toUpperCase().replaceAll("[^A-Z]", "");

        String tmp = new StringBuilder(str).reverse().toString();

        //equalsIgnoreCase 알파벳 대소문자 무시
        if(str.equalsIgnoreCase(tmp)) answer = "YES";

        return answer;
    }
}
```

---

## 9. 숫자만 추출

- 설명

문자와 숫자가 섞여있는 문자열이 주어지면 그 중 숫자만 추출하여 그 순서대로 자연수를 만듭니다.

만약 “tge0a1h205er”에서 숫자만 추출하면 0, 1, 2, 0, 5이고 이것을 자연수를 만들면 1205이 됩니다.

추출하여 만들어지는 자연수는 100,000,000을 넘지 않습니다.

- 입력

첫 줄에 숫자가 썩인 문자열이 주어집니다. 문자열의 길이는 100을 넘지 않습니다.

- 출력

첫 줄에 자연수를 출력합니다.

1. 예시1 (내풀이)

```java
package BaekJoon;

import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.nextLine();
        System.out.println(solution(str));
    }

    public static int solution(String str){
        String answer = "";
        str = str.replaceAll("[^0-9]", "");
        answer = str;

        return Integer.parseInt(answer);
    }
}
```

1. 예시2

```java
package BaekJoon;

import java.util.*;

/*
answer 에 중첩
ex) 0 * 10 (48 - 48) -> 1 * 10 + (49 - 48) 이런식으로 반복
*/
public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.nextLine();
        System.out.println(solution(str));
    }

    public static int solution(String str){
        int answer = 0;

        for(char c : str.toCharArray()){
            if(c>=48 && c<=57) answer = answer * 10 + (c-48);
        }

        return answer;
    }
}
```

---

## 10. 가장 짧은 문자거리

- 설명

한 개의 문자열 s와 문자 t가 주어지면 문자열 s의 각 문자가 문자 t와 떨어진 최소거리를 출력하는 프로그램을 작성하세요.

- 입력

첫 번째 줄에 문자열 s와 문자 t가 주어진다. 문자열과 문자는 소문자로만 주어집니다.

문자열의 길이는 100을 넘지 않는다.

- 출력

첫 번째 줄에 각 문자열 s의 각 문자가 문자 t와 떨어진 거리를 순서대로 출력한다.

```java
package BaekJoon;

import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.next();
        char c = scanner.next().charAt(0);

        for(int i : solution(str,c)){
            System.out.print(i + " ");
        }
    }

    public static int[] solution(String str, char c){
        int [] answer = new int[str.length()];
        int p = 1000;

        for(int i=0; i<str.length(); i++){
            if(str.charAt(i)==c){
                p = 0;
            }else{
                p++;
            }
            answer[i] = p;
        }

        p = 1000;
        for(int i =str.length() - 1; i>=0; i--){
            if(str.charAt(i)==c){
                p = 0;
            }else{
                p++;
                answer[i] = Math.min(answer[i], p);
            }
        }
        return answer;
    }
}
```

- 풀이

answer 배열을 생성 → 

p = 1000으로 설정(왼쪽이나 오른쪽에 타겟문자가 없을경우 거리를 큰 숫자로 해야 반대방향의 거리가 작은값이 되어 선택되게됨.) → 

문자를 하나씩 스캔하면서 같을시 0 으로 지정 아닐시 p++ 하여 배열 인덱스에 p 를 저장 →

두번째 반복문은 배열 인덱스 뒤에부분에서 스캔 시작해서 가까운 타겟문자와 값이 같을시에 0 으로지정 아닐시에 p++ 

하여 배열 인덱스에 새롭게 저장→ return

---

## 11. 문자열 압축

- 설명

알파벳 대문자로 이루어진 문자열을 입력받아 같은 문자가 연속으로 반복되는 경우 반복되는

문자 바로 오른쪽에 반복 횟수를 표기하는 방법으로 문자열을 압축하는 프로그램을 작성하시오.

단 반복횟수가 1인 경우 생략합니다.

- 입력

첫 줄에 문자열이 주어진다. 문자열의 길이는 100을 넘지 않는다.

- 출력

첫 줄에 압축된 문자열을 출력한다.

```java
package BaekJoon;

import java.util.*;

/*
예시입력 : KKHSSSSSSSE
출력예시 : K2HS7E
*/
public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.next();
        System.out.println(solution(str));
    }

    public static String solution(String str){
        String answer = "";
        str = str + " ";
        int cnt = 1;

        //str 에서 빈문자 하나 추가했으므로 - 1
        for(int i=0; i<str.length() - 1; i++){
            if(str.charAt(i) == str.charAt(i + 1)){
                cnt++;
            }else{
                answer += str.charAt(i);
                if(cnt > 1){
                    answer += cnt;
                    cnt = 1;
                }
            }
        }
        return answer;
    }
}
```

- 풀이

str 에서 마지막에 공백추가(i + 1 했으므로 배열 오류 방지)→

i 와 i + 1 이 같으면 cnt++ 처리 다를시 answer 에 해당 문자 중첩저장 →

cnt 가 1 이상이면 answer 에 cnt 중첩저장후 cnt=1 로 초기화→ return

---

## 12. 암호

- 설명

현수는 영희에게 알파벳 대문자로 구성된 비밀편지를 매일 컴퓨터를 이용해 보냅니다.

비밀편지는 현수와 영희가 서로 약속한 암호로 구성되어 있습니다.

비밀편지는 알파벳 한 문자마다 # 또는 *이 일곱 개로 구성되어 있습니다.

만약 현수가 “#*****#”으로 구성된 문자를 보냈다면 영희는 현수와 약속한 규칙대로 다음과 같이 해석합니다.

1. “#*****#”를 일곱자리의 이진수로 바꿉니다. #은 이진수의 1로, *이진수의 0으로 변환합니다. 결과는 “1000001”로 변환됩니다.

2. 바뀐 2진수를 10진수화 합니다. “1000001”을 10진수화 하면 65가 됩니다.

3. 아스키 번호가 65문자로 변환합니다. 즉 아스크번호 65는 대문자 'A'입니다.

참고로 대문자들의 아스키 번호는 'A'는 65번, ‘B'는 66번, ’C'는 67번 등 차례대로 1씩 증가하여 ‘Z'는 90번입니다.

현수가 4개의 문자를 다음과 같이 신호로 보냈다면

#****###**#####**#####**##**

이 신호를 4개의 문자신호로 구분하면

#****## --> 'C'

#**#### --> 'O'

#**#### --> 'O'

#**##** --> 'L'

최종적으로 “COOL"로 해석됩니다.

현수가 보낸 신호를 해석해주는 프로그램을 작성해서 영희를 도와주세요.

- 입력

첫 줄에는 보낸 문자의 개수(10을 넘지 안습니다)가 입력된다. 다음 줄에는 문자의 개수의 일곱 배 만큼의 #또는 * 신호가 입력됩니다.

현수는 항상 대문자로 해석할 수 있는 신호를 보낸다고 가정합니다.

- 출력

영희가 해석한 문자열을 출력합니다

```java
package BaekJoon;

import java.util.*;

/*
예시입력 : 4
#****###**#####**#####**##**
출력예시 : COOL 

*/
public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int i = scanner.nextInt();
        String str = scanner.next();
        System.out.println(solution(i,str).toUpperCase());

    }

    public static String solution(int num, String str){
        String answer = "";

        for(int i=0; i<num; i++){
            str = str.replace("#" , "1");
            str = str.replace("*" , "0");

            String tmp = str.substring(0,7);
            str = str.substring(7);

            int num2 = Integer.parseInt(tmp, 2);
            answer += (char)num2;
        }

        return answer;
    }
}
```

 

- 풀이

replace 메소드를 이용 “#” , “*” 2진법으로 변환 →

tmp 에 subString 이용 잘라서 저장 →

중복 문자열 저장 안되게 str 에 subString 7 으로 다시 치환→

2진수화 → 문자로 return

  

---

## **Array(1, 2차원 배열)**

### 1. 큰 수 출력하기

- 설명

N개의 정수를 입력받아, 자신의 바로 앞 수보다 큰 수만 출력하는 프로그램을 작성하세요.

(첫 번째 수는 무조건 출력한다)

- 입력

첫 줄에 자연수 N(1<=N<=100)이 주어지고, 그 다음 줄에 N개의 정수가 입력된다.

- 출력

자신의 바로 앞 수보다 큰 수만 한 줄로 출력한다.

```java
package BaekJoon;

import java.util.*;

/*
* 예시 입력 : 6
7 3 9 5 6 12
* 예시 출력 : 7 9 6 12
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();
        int [] arr = new int[num];

        for(int i=0; i<arr.length; i++){
            arr[i] = scanner.nextInt();
        }
        for(int x : solution(num, arr)){
            System.out.print(x + " ");
        }
    }
    public static ArrayList<Integer> solution(int n, int[] arr){
        ArrayList<Integer> answer = new ArrayList<>();
        answer.add(arr[0]);

        for(int i=1; i<n; i++){
            if(arr[i] > arr[i-1]){
              answer.add(arr[i]);
            }
        }
        return answer;
    }
}
```

---

### 2. 보이는 학생

- 설명

선생님이 N명의 학생을 일렬로 세웠습니다. 일렬로 서 있는 학생의 키가 앞에서부터 순서대로 주어질 때, 맨 앞에 서 있는

선생님이 볼 수 있는 학생의 수를 구하는 프로그램을 작성하세요. (앞에 서 있는 사람들보다 크면 보이고, 작거나 같으면 보이지 않습니다.)

- 입력

첫 줄에 정수 N(5<=N<=100,000)이 입력된다. 그 다음줄에 N명의 학생의 키가 앞에서부터 순서대로 주어진다.

- 출력

선생님이 볼 수 있는 최대학생수를 출력한다.

```java
package BaekJoon;

import java.util.*;

/*
* 이중 포문 O(n2) -> X
*
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();
        int [] arr = new int[num];

        for(int i=0; i<arr.length; i++){
            arr[i] = scanner.nextInt();
        }
        System.out.println(solution(num, arr));
    }

    public static int solution(int n, int[] arr){
        int answer = 1;
        int max = arr[0];

        for(int i=1; i<n; i++){
            if(max < arr[i]){
                max = arr[i];
                answer++;
            }
        }
        return answer;
    }
}
```

---

### 3. 가위바위보

- 설명

A, B 두 사람이 가위바위보 게임을 합니다. 총 N번의 게임을 하여 A가 이기면 A를 출력하고, B가 이기면 B를 출력합니다. 비길 경우에는 D를 출력합니다.

가위, 바위, 보의 정보는 1:가위, 2:바위, 3:보로 정하겠습니다.

예를 들어 N=5이면

![https://cote.inflearn.com/public/upload/a48402588b.jpg](https://cote.inflearn.com/public/upload/a48402588b.jpg)

두 사람의 각 회의 가위, 바위, 보 정보가 주어지면 각 회를 누가 이겼는지 출력하는 프로그램을 작성하세요.

- 입력

첫 번째 줄에 게임 횟수인 자연수 N(1<=N<=100)이 주어집니다.

두 번째 줄에는 A가 낸 가위, 바위, 보 정보가 N개 주어집니다.

세 번째 줄에는 B가 낸 가위, 바위, 보 정보가 N개 주어집니다.

- 출력

```java
package BaekJoon;

import java.util.*;

public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();
        int [] arr = new int[num];
        int [] arr2 = new int[num];

        for(int i=0; i<arr.length; i++){
            arr[i] = scanner.nextInt();
        }

        for(int i=0; i<arr.length; i++){
            arr2[i] = scanner.nextInt();
        }

        for(char x : solution(num, arr, arr2).toCharArray()){
            System.out.println(x);
        }
    }

    public static String solution(int n, int[] arr, int[] arr2){
        String answer = "";

        for(int i=0; i<n; i++){
            if(arr[i] == arr2[i]){
                answer+= "D";
            }else if(arr[i] == 1 && arr2[i] == 3){
                answer+= "A";
            }else if(arr[i] == 2 && arr2[i] == 1){
                answer+= "A";
            }else if(arr[i] == 3 && arr2[i] == 2){
                answer+= "A";
            }else{
                answer+= "B";
            }
        }
        return answer;
   
```

---

### 4. 피보나치 수열

- 설명

1) 피보나키 수열을 출력한다. 피보나치 수열이란 앞의 2개의 수를 합하여 다음 숫자가 되는 수열이다.

2) 입력은 피보나치 수열의 총 항의 수 이다. 만약 7이 입력되면 1 1 2 3 5 8 13을 출력하면 된다.

- 입력

첫 줄에 총 항수 N(3<=N<=45)이 입력된다.

- 출력

첫 줄에 피보나치 수열을 출력합니다.

```java
package BaekJoon;

import java.util.*;

/*
* 입력 예시 : 10
* 출력 예시 : 1 1 2 3 5 8 13 21 34 55
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();

        for(int i : solution(num)){
            System.out.print(i + " ");
        }

    }

    public static int[] solution(int n){
        int[] answer = new int[n];

        answer[0] = 1;
        answer[1] = 1;

        for(int i=0; i<n-2; i++){
            answer[i+2] = answer[i] + answer[i+1];
        }

        return answer;
    }
}
```

---

## 5. 소수

설명

자연수 N이 입력되면 1부터 N까지의 소수의 개수를 출력하는 프로그램을 작성하세요.

만약 20이 입력되면 1부터 20까지의 소수는 2, 3, 5, 7, 11, 13, 17, 19로 총 8개입니다.

입력

첫 줄에 자연수의 개수 N(2<=N<=200,000)이 주어집니다.

출력

첫 줄에 소수의 개수를 출력합니다.

1. 예시 1

```java
package BaekJoon;

import java.util.*;

/*
* 입력 예시 : 20
* 출력 예시 : 8
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();

        System.out.println(solution(num));

    }

    public static int solution(int n){
        int answer = 0;
        int count = 0;

        for(int i=2; i<=n; i++){
            for(int j=2; j<=i; j++){
                if(i%j==0){
                    count++;
                }
            }

            if(count ==1){
                answer++;
            }
            count=0;
        }

        return answer;
    }
}
```

- 이렇게 푸니까 런타임 오류 발생,,

1. 예시2

```java
package BaekJoon;

import java.util.*;

/*
* 입력 예시 : 20
* 출력 예시 : 8
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();

        System.out.println(solution(num));

    }

    public static int solution(int n){
        int answer = 0;
        int [] ch = new int[n + 1];

        for(int i=2; i<=n; i++){
            if(ch[i] == 0){
                answer++;
                for(int j=i; j<=n; j=j+i)
                    ch[j] = 1;
            }
        }
        return answer;
    }
}
```

- 풀이

ch 배열에 n+1 만큼 배열 생성 →

i 를 2로 지정 만약 ch[i] == 0이면 (소수) answer++ 약수가 있는 경우는 배열에서 1로 초기화→

return

---

## 6. 뒤집은 소수

설명

N개의 자연수가 입력되면 각 자연수를 뒤집은 후 그 뒤집은 수가 소수이면 그 소수를 출력하는 프로그램을 작성하세요.

예를 들어 32를 뒤집으면 23이고, 23은 소수이다. 그러면 23을 출력한다. 단 910를 뒤집으면 19로 숫자화 해야 한다.

첫 자리부터의 연속된 0은 무시한다.

입력

첫 줄에 자연수의 개수 N(3<=N<=100)이 주어지고, 그 다음 줄에 N개의 자연수가 주어진다.

각 자연수의 크기는 100,000를 넘지 않는다.

출력

첫 줄에 뒤집은 소수를 출력합니다. 출력순서는 입력된 순서대로 출력합니다.

```java
package BaekJoon;

import java.util.*;

/*
* 입력 예시 : 9
32 55 62 20 250 370 200 30 100

* 출력 예시 : 23 2 73 2 3
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();
        int [] arr = new int[num];

        for(int i=0; i<arr.length; i++){
            arr[i] = scanner.nextInt();
        }
        for(int x : solution(num, arr)){
            System.out.print(x + " ");
        }
    }

    public static ArrayList<Integer> solution(int n, int[] arr){
        ArrayList<Integer> answer = new ArrayList<>();

        for(int i=0; i<n; i++){
            int tmp = arr[i];
            int res = 0;
            /**
             * 숫자를 뒤집어 주는 로직
             * ex) t = 123 % 10 => t = 3;
             *  res = 0 * 10 + t => 3
             *  tmp = 123 / 10 => 12
             *  이 방식으로 계속 반복 => 다 뒤집으면 321
             */
            while (tmp > 0){
                int t = tmp % 10;
                res = res * 10 + t;
                tmp = tmp / 10;
            }
            if(isPrime(res)) answer.add(res);
        }
        return answer;
    }

    public static boolean isPrime(int num){
        if(num == 1) return false;
        for(int i =2; i<num; i++){
            if(num % i == 0){ //소수가 아님(약수임)
                return false;
            }
        }
        return true;
    }
}
```

- 풀이

solution 메서드에서 배열을 시그니처로 받음 →

숫자 뒤집는 로직 생성 →  isPrime 소수 인지 체크하는 메서드 생성 →

for 문을 돌려서 소수이면 true 아닐시 false → 배열에 소수 인자 추가 → return

---

## 7. 점수계산

설명

OX 문제는 맞거나 틀린 두 경우의 답을 가지는 문제를 말한다.

여러 개의 OX 문제로 만들어진 시험에서 연속적으로 답을 맞히는 경우에는 가산점을 주기 위해서 다음과 같이 점수 계산을 하기로 하였다.

1번 문제가 맞는 경우에는 1점으로 계산한다. 앞의 문제에 대해서는 답을 틀리다가 답이 맞는 처음 문제는 1점으로 계산한다.

또한, 연속으로 문제의 답이 맞는 경우에서 두 번째 문제는 2점, 세 번째 문제는 3점, ..., K번째 문제는 K점으로 계산한다. 틀린 문제는 0점으로 계산한다.

예를 들어, 아래와 같이 10 개의 OX 문제에서 답이 맞은 문제의 경우에는 1로 표시하고, 틀린 경우에는 0으로 표시하였을 때,

점수 계산은 아래 표와 같이 계산되어, 총 점수는 1+1+2+3+1+2=10 점이다.

![https://cote.inflearn.com/public/upload/6080c8e8dc.jpg](https://cote.inflearn.com/public/upload/6080c8e8dc.jpg)

시험문제의 채점 결과가 주어졌을 때, 총 점수를 계산하는 프로그램을 작성하시오.

입력

첫째 줄에 문제의 개수 N (1 ≤ N ≤ 100)이 주어진다. 둘째 줄에는 N개 문제의 채점 결과를 나타내는 0 혹은 1이 빈 칸을 사이에 두고 주어진다.

0은 문제의 답이 틀린 경우이고, 1은 문제의 답이 맞는 경우이다.

출력

첫째 줄에 입력에서 주어진 채점 결과에 대하여 가산점을 고려한 총 점수를 출력한다.

1. 내풀이

```java
package BaekJoon;

import java.util.*;

/*
* 입력 예시 : 10
1 0 1 1 1 0 0 1 1 0
* 출력 예시 : 10
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();
        int [] arr = new int[num];

        for(int i=0; i<arr.length; i++){
            arr[i] = scanner.nextInt();
        }

        System.out.println(solution(num, arr));
    }

    public static int solution(int num, int [] arr){
        int answer = 0;
        int tmp = 0;

        for(int i=0; i<num; i++){
            if(arr[i] == 1){
                tmp += 1;
                answer += tmp;
            }else{
                tmp = 0;
            }
        }
        return answer;
    }
}
```

---

## 8. 등수구하기

설명

N명의 학생의 국어점수가 입력되면 각 학생의 등수를 입력된 순서대로 출력하는 프로그램을 작성하세요.

같은 점수가 입력될 경우 높은 등수로 동일 처리한다.

즉 가장 높은 점수가 92점인데 92점이 3명 존재하면 1등이 3명이고 그 다음 학생은 4등이 된다.

입력

첫 줄에 N(3<=N<=100)이 입력되고, 두 번째 줄에 국어점수를 의미하는 N개의 정수가 입력된다.

출력

입력된 순서대로 등수를 출력한다.

```java
package BaekJoon;

import java.util.*;

/*
* 입력 예시 : 5
87 89 92 100 76

* 출력 예시 : 4 3 2 1 5
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();
        int [] arr = new int[num];

        for(int i=0; i<arr.length; i++){
            arr[i] = scanner.nextInt();
        }

        for(int x : solution(arr)){
            System.out.print(x + " ");
        }
    }

    public static ArrayList<Integer> solution(int[] arr){
        ArrayList<Integer> answer = new ArrayList<>();

        for(int i=0; i<arr.length; i++){
            int cnt = 1;
            for(int j=0; j<arr.length; j++){
                if(arr[i] < arr[j]) cnt++;
            }
            answer.add(cnt);
        }
        return answer;
    }
}
```

- 풀이

solution 메서드에서 배열로 시그니처를 받음 →

2중 for 문을 돌려서  받은 시그니처의 배열끼리 비교 후 cnt++→  answer 배열에 담아준다 → return ;

---

## 9. 격자판 최대합

설명

5*5 격자판에 아래롸 같이 숫자가 적혀있습니다.

![https://cote.inflearn.com/public/upload/4897574b00.jpg](https://cote.inflearn.com/public/upload/4897574b00.jpg)

N*N의 격자판이 주어지면 각 행의 합, 각 열의 합, 두 대각선의 합 중 가 장 큰 합을 출력합니다.

입력

첫 줄에 자연수 N이 주어진다.(2<=N<=50)

두 번째 줄부터 N줄에 걸쳐 각 줄에 N개의 자연수가 주어진다. 각 자연수는 100을 넘지 않는다.

출력

최대합을 출력합니다.

1. 예시1

```java
package BaekJoon;

import java.util.*;

/*
* 입력 예시 : 5
10 13 10 12 15
12 39 30 23 11
11 25 50 53 15
19 27 29 37 27
19 13 30 13 19

* 출력 예시 : 154
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();
        int [][] arr = new int[num][num];

        for(int i=0; i<num; i++){
            for(int j=0; j<num; j++){
                arr[i][j] = scanner.nextInt();
            }
        }
        System.out.println(solution(arr));
    }

    public static int solution(int[][] arr){
        int answer= 0;

        for(int i=0; i<arr.length; i++){
            int tmp= 0;
            int tmp1= 0;
            for(int j=0; j<arr.length; j++){
                tmp += arr[i][j];
                tmp1 += arr[j][i];
            }
            answer = Math.max(answer, tmp);
            answer = Math.max(answer, tmp1);
        }

        for(int i=0; i<arr.length; i++){
            int tmp3 =0;
            int tmp4 =0;

            tmp3 += arr[i][i];
            tmp4 += arr[i][arr.length - i - 1];

            Math.max(answer, tmp3);
            Math.max(answer, tmp4);
        }
       return answer;
    }
}
```

- 풀이

for 문으로 배열 돌려서 가로 세로 합 → arr[i][i] 를 통해서 왼쪽에서 오른쪽 대각선 값 → arr[i][arr.length - i - 1] 를 통해서 반대 대각선 합 → Math.max 통해 큰값 구해서 return;

---

## 10. 봉우리

설명

지도 정보가 N*N 격자판에 주어집니다. 각 격자에는 그 지역의 높이가 쓰여있습니다.

각 격자판의 숫자 중 자신의 상하좌우 숫자보다 큰 숫자는 봉우리 지역입니다. 봉우리 지역이 몇 개 있는 지 알아내는 프로그램을 작성하세요.

격자의 가장자리는 0으로 초기화 되었다고 가정한다.

만약 N=5 이고, 격자판의 숫자가 다음과 같다면 봉우리의 개수는 10개입니다.

![https://cote.inflearn.com/public/upload/d0a3fd4667.jpg](https://cote.inflearn.com/public/upload/d0a3fd4667.jpg)

입력

첫 줄에 자연수 N이 주어진다.(2<=N<=50)

두 번째 줄부터 N줄에 걸쳐 각 줄에 N개의 자연수가 주어진다. 각 자연수는 100을 넘지 않는다.

출력

봉우리의 개수를 출력하세요.

1. 예시1

```java
package BaekJoon;

import java.util.*;

/*
* 입력 예시 : 5
5 3 7 2 3
3 7 1 6 1
7 2 5 3 4
4 3 6 4 1
8 7 3 5 2

* 출력 예시 : 10
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();
        int [][] arr = new int[num+2][num+2];

        for(int i=1; i<num+1; i++){
            for(int j=1; j<num+1; j++){
                arr[i][j] = scanner.nextInt();
            }
        }
        System.out.println(solution(num,arr));
    }

    public static int solution(int num, int[][] arr){
        int answer= 0;

        for(int i=1; i<=num; i++){
            for(int j=1; j<=num; j++){
                if(arr[i][j] > arr[i-1][j] && arr[i][j] > arr[i+1][j] && arr[i][j] > arr[i][j-1] && arr[i][j] > arr[i][j+1]){
                    answer++;
                }
            }
        }
       return answer;
    }
}
```

- 풀이

2.예시2

```java
package BaekJoon;

import java.util.*;

/*
* 입력 예시 : 5
5 3 7 2 3
3 7 1 6 1
7 2 5 3 4
4 3 6 4 1
8 7 3 5 2

* 출력 예시 : 10
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();
        int [][] arr = new int[num][num];

        for(int i=0; i<num; i++){
            for(int j=0; j<num; j++){
                arr[i][j] = scanner.nextInt();
            }
        }
        System.out.println(solution(num,arr));
    }

    public static int solution(int num, int[][] arr){
        int answer= 0;

				//네 방향 좌표
        int [] dx = {-1, 0, 1, 0};
        int [] dy = {0, 1, 0, -1};

        for(int i=0; i<num; i++){
            for(int j=0; j<num; j++){
                boolean flag = true;
                for(int k=0; k<4; k++){
                    int nx = i+dx[k]; //행 좌표
                    int ny = j+dy[k]; //열 좌표
                    //인덱스 바운더리 오류 방지
                    if(nx >=0 && nx < num && ny >= 0 && ny < num && arr[nx][ny] >= arr[i][j]){
                        flag = false;
                        break;
                    }
                }
                if(flag) answer++;
            }
        }
       return answer;
    }
}
```

- 풀이

좌표로 dx , dy 초기화 → 

int nx = i + dx[k] → int ny = j + dy[k] → for 문 돌려서 좌표대로 하나씩 비교 → return;

---

## 11. 임시반장 정하기

설명

김갑동 선생님은 올해 6학년 1반 담임을 맡게 되었다.

김갑동 선생님은 우선 임시로 반장을 정하고 학생들이 서로 친숙해진 후에 정식으로 선거를 통해 반장을 선출하려고 한다.

그는 자기반 학생 중에서 1학년부터 5학년까지 지내오면서 한번이라도 같은 반이었던 사람이 가장 많은 학생을 임시 반장으로 정하려 한다.

그래서 김갑동 선생님은 각 학생들이 1학년부터 5학년까지 몇 반에 속했었는지를 나타내는 표를 만들었다.

예를 들어 학생 수가 5명일 때의 표를 살펴보자.

![https://cote.inflearn.com/public/upload/f8a83920ca.jpg](https://cote.inflearn.com/public/upload/f8a83920ca.jpg)

위 경우에 4번 학생을 보면 3번 학생과 2학년 때 같은 반이었고, 3번 학생 및 5번 학생과 3학년 때 같은 반이었으며,

2번 학생과는 4학년 때 같은 반이었음을 알 수 있다. 그러므로 이 학급에서 4번 학생과 한번이라도

같은 반이었던 사람은 2번 학생, 3번 학생과 5번 학생으로 모두 3명이다.

이 예에서 4번 학생이 전체 학생 중에서 같은 반이었던 학생 수가 제일 많으므로 임시 반장이 된다.

각 학생들이 1학년부터 5학년까지 속했던 반이 주어질 때, 임시 반장을 정하는 프로그램을 작성하시오.

입력

첫째 줄에는 반의 학생 수를 나타내는 정수가 주어진다. 학생 수는 3 이상 1000 이하이다.

둘째 줄부터는 1번 학생부터 차례대로 각 줄마다 1학년부터 5학년까지 몇 반에 속했었는지를 나타내는 5개의 정수가 빈칸 하나를 사이에 두고 주어진다.

주어지는 정수는 모두 1 이상 9 이하의 정수이다.

출력

첫 줄에 임시 반장으로 정해진 학생의 번호를 출력한다.

단, 임시 반장이 될 수 있는 학생이 여러 명인 경우에는 그 중 가장 작은 번호만 출력한다.

```java
package BaekJoon;

import java.util.*;

/*
* 입력 예시 : 5
2 3 1 7 3
4 1 9 6 8
5 5 2 4 4
6 5 2 6 7
8 4 2 2 2

* 출력 예시 : 4
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();

        //i 부분 동적으로 하기위해 , 1학년에서부터 5학년까지 배열생성
        int [][] arr = new int[num+1][6];

        //1부터 값을 넣는다.
        for(int i=1; i<num; i++){
            for(int j=1; j<=5; j++){
                arr[i][j] = scanner.nextInt();
            }
        }
        System.out.println(solution(num,arr));
    }

    public static int solution(int num, int[][] arr){
        int answer=0, min=Integer.MIN_VALUE;

        for(int i=1; i<=num; i++){
            int cnt = 0;
            for(int j=1; j<=num; j++){
                //1학년때부터 5학년까지 k for 문
                for(int k =1; k<=5; k++){
                    if(arr[i][k] == arr[j][k]){
                        cnt++;
                        break;
                    }
                }
            }
            if(cnt > min){
                min = cnt;
                answer = i;
            }
        }
       return answer;
    }
}
```

- 풀이

1번부터 사용하므로 arr[n+1][6] 으로 2차원 배열 생성 →

for문으로 1학년 부터 i → j → k → 순서대로 반복문 i 가 1일때 j 가 1 , 2 , 3, 4, 5 같은반 했던 j 학생  →

j 번 학생이 i 반 학생과 같은반인지 k 로 for 문 a[i][k] == a[j][k] k 학년에 반이 같은지 같으면 ? cnt++ →

자기와 자기자신 비교해도 상관X ⇒ 학생수가 아니라 그 학생을 찾는 문제임 →

한번만 비교되게 break 추가 → return;

---

## 12 . 멘토링(브루트포스)

설명

현수네 반 선생님은 반 학생들의 수학점수를 향상시키기 위해 멘토링 시스템을 만들려고 합니다.

멘토링은 멘토(도와주는 학생)와 멘티(도움을 받는 학생)가 한 짝이 되어 멘토가 멘티의 수학공부를 도와주는 것입니다.

선생님은 M번의 수학테스트 등수를 가지고 멘토와 멘티를 정합니다.

만약 A학생이 멘토이고, B학생이 멘티가 되는 짝이 되었다면, A학생은 M번의 수학테스트에서 모두 B학생보다 등수가 앞서야 합니다.

M번의 수학성적이 주어지면 멘토와 멘티가 되는 짝을 만들 수 있는 경우가 총 몇 가지 인지 출력하는 프로그램을 작성하세요.

입력
첫 번째 줄에 반 학생 수 N(1<=N<=20)과 M(1<=M<=10)이 주어진다.

두 번째 줄부터 M개의 줄에 걸쳐 수학테스트 결과가 학생번호로 주어진다. 학생번호가 제일 앞에서부터 1등, 2등, ...N등 순으로 표현된다.

만약 한 줄에 N=4이고, 테스트 결과가 3 4 1 2로 입력되었다면 3번 학생이 1등, 4번 학생이 2등, 1번 학생이 3등, 2번 학생이 4등을 의미합니다.

출력
첫 번째 줄에 짝을 만들 수 있는 총 경우를 출력합니다.

```java
package Main;

import java.util.Scanner;

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
        int n = scanner.nextInt();
        int m = scanner.nextInt();

        int [][] arr = new int[m][n];

        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                arr[i][j] = scanner.nextInt();
            }
        }
        System.out.println(solution(n,m, arr));
    }

    public static int solution(int n, int m, int[][] arr){
        int answer=0;

        // 학생 수 만큼 -> 1번 부터 시작 (학생번호)
        for(int i=1; i<=n; i++){ //멘토
            for(int j=1; j<=n; j++){ //멘티
                int cnt = 0;

                // i 와 j 멘토 멘티가 될수있는지 검증
                // 테스트 수 만큼
                for(int k=0; k<m; k++){
                    int mentor=0, mentee=0;
                    // 등 수 만큼(학생 수)
                    for(int s=0; s<n; s++){
                        // 해당 위치에 본인 번호가 있으면 본인은 s등 이다.
                        if(arr[k][s] == i) mentor = s;
                        if(arr[k][s] == j) mentee = s;
                    }
                    //멘토가 등수가 더 높으면
                    if(mentor<mentee) cnt++;
                }
                if(cnt == m) answer++; // 멘토가 모든시험에서 앞서면
            }
        }
       return answer;
    }
```

---
