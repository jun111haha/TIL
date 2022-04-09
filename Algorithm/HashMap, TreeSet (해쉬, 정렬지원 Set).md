### 1. **학급 회장(해쉬)**

설명

학급 회장을 뽑는데 후보로 기호 A, B, C, D, E 후보가 등록을 했습니다.

투표용지에는 반 학생들이 자기가 선택한 후보의 기호(알파벳)가 쓰여져 있으며 선생님은 그 기호를 발표하고 있습니다.

선생님의 발표가 끝난 후 어떤 기호의 후보가 학급 회장이 되었는지 출력하는 프로그램을 작성하세요.

반드시 한 명의 학급회장이 선출되도록 투표결과가 나왔다고 가정합니다.

입력

첫 줄에는 반 학생수 N(5<=N<=50)이 주어집니다.

두 번째 줄에 N개의 투표용지에 쓰여져 있던 각 후보의 기호가 선생님이 발표한 순서대로 문자열로 입력됩니다.

출력

학급 회장으로 선택된 기호를 출력합니다.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
15
BACBACCACCBDEDE

* 출력 예시 : C
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();
        String str = scanner.next();

        System.out.println(solution(num, str));
    }

    public static char solution(int n, String str){
        char answer = ' ';

        HashMap<Character, Integer> map = new HashMap<>();
        for(char x : str.toCharArray()){
            map.put(x, map.getOrDefault(x, 0) + 1);
        }
				//{A=3, B=3, C=5, D=2, E=2} 으로 반환

        int max = Integer.MIN_VALUE;
        for(char key : map.keySet()){
            if(max < map.get(key)){
                max = map.get(key);
                answer = key;
            }
        }

        return answer;
    }
}
```

- 풀이
    
    **getOrDefault(**Object key, V DefaultValue**)**
    
    **매개 변수 :** 이 메서드는 두 개의 매개 변수를 허용합니다.
    
    - **key :** 값을 가져와야 하는 요소의 **키입니다.**
    - **defaultValue :** 지정된 키로 매핑된 값이 없는 경우 반환되어야 하는 **기본값입니다.**
    
    **반환 값 :** 찾는 key가 존재하면 해당 key에 매핑되어 있는 값을 반환하고, 그렇지 않으면 **디폴트 값이** 반환됩니다.
    
    HashMap의 경우 동일 키 값을 추가할 경우 Value의 값이 덮어쓰기가 됩니다. 따라서 기존 key 값의 value를 계속 사용하고 싶을 경우 getOrDefault 메서드를 사용하여 위의 예와 같이 사용할 수 있습니다.
    
    getOrDefault 메서드 사용 str 를 map 형태로 키 값 반환 → max 값 지정 for 문돌려서 map 에서 제일 큰 밸류값의 키를 찾는다 →
    
    return;
    

---

### 2. 아나그램(해쉬)

설명

Anagram이란 두 문자열이 알파벳의 나열 순서를 다르지만 그 구성이 일치하면 두 단어는 아나그램이라고 합니다.

예를 들면 AbaAeCe 와 baeeACA 는 알파벳을 나열 순서는 다르지만 그 구성을 살펴보면 A(2), a(1), b(1), C(1), e(2)로

알파벳과 그 개수가 모두 일치합니다. 즉 어느 한 단어를 재 배열하면 상대편 단어가 될 수 있는 것을 아나그램이라 합니다.

길이가 같은 두 개의 단어가 주어지면 두 단어가 아나그램인지 판별하는 프로그램을 작성하세요. 아나그램 판별시 대소문자가 구분됩니다.

입력

첫 줄에 첫 번째 단어가 입력되고, 두 번째 줄에 두 번째 단어가 입력됩니다.

단어의 길이는 100을 넘지 않습니다.

출력

두 단어가 아나그램이면 “YES"를 출력하고, 아니면 ”NO"를 출력합니다.

1. 예시1(내풀이)

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
AbaAeCe
baeeACA

* 출력 예시 : YES
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        String str1 = scanner.next();
        String str2 = scanner.next();

        System.out.println(solution(str1, str2));
    }

    public static String solution(String str1, String str2){
        String answer = "YES";

        HashMap<Character, Integer> map = new HashMap<>();
        HashMap<Character, Integer> map2 = new HashMap<>();

        for(char x : str1.toCharArray()){ 
            // 해당 문자를 가지고 있지 않으면
            if(!map.containsKey(x)){
            // 새로 저장한 후 1로 초기화
                map.put(x, 1);
            // 해당 문자를 가지고 있으면 기존값에 1더하기
            }else{
                map.put(x, map.get(x) +1);
            }
        }

        for(char y : str2.toCharArray()){
            if(!map2.containsKey(y)){
                map2.put(y, 1);
            }else{
                map2.put(y, map2.get(y) +1);
            }
        }

        /* map, map1 출력 결과
        * {A=2, a=1, b=1, C=1, e=2}
          {a=1, A=2, b=1, C=1, e=2}
        * */

        for(char x : map.keySet()){
            if(map.get(x) != map2.get(x)){
                answer = "NO";
                return answer;
            }
        }

        return answer;
    }
}
```

1. 예시2

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
AbaAeCe
baeeACA

* 출력 예시 : YES
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        String str1 = scanner.next();
        String str2 = scanner.next();

        System.out.println(solution(str1, str2));
    }

    public static String solution(String str1, String str2){
        String answer = "YES";
        HashMap<Character, Integer> map = new HashMap<>();

        for(char x : str1.toCharArray()){
            map.put(x, map.getOrDefault(x, 0) + 1);
        }

        for(char x : str2.toCharArray()){
            if(!map.containsKey(x) || map.get(x) == 0){
                return "NO";
            }
						map.put(x, map.get(x) - 1);
        }

        return answer;
    }
}
```

- 풀이

---

### 3. 매출액의 종류(Hash, Sliding Window)

설명

현수의 아빠는 제과점을 운영합니다. 현수아빠는 현수에게 N일 동안의 매출기록을 주고 연속된 K일 동안의 매출액의 종류를

각 구간별로 구하라고 했습니다.

만약 N=7이고 7일 간의 매출기록이 아래와 같고, 이때 K=4이면

20 12 20 10 23 17 10

각 연속 4일간의 구간의 매출종류는

첫 번째 구간은 [20, 12, 20, 10]는 매출액의 종류가 20, 12, 10으로 3이다.

두 번째 구간은 [12, 20, 10, 23]는 매출액의 종류가 4이다.

세 번째 구간은 [20, 10, 23, 17]는 매출액의 종류가 4이다.

네 번째 구간은 [10, 23, 17, 10]는 매출액의 종류가 3이다.

N일간의 매출기록과 연속구간의 길이 K가 주어지면 첫 번째 구간부터 각 구간별

매출액의 종류를 출력하는 프로그램을 작성하세요.

입력

첫 줄에 N(5<=N<=100,000)과 K(2<=K<=N)가 주어집니다.

두 번째 줄에 N개의 숫자열이 주어집니다. 각 숫자는 500이하의 음이 아닌 정수입니다.

출력

첫 줄에 각 구간의 매출액 종류를 순서대로 출력합니다.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
7 4
20 12 20 10 23 17 10
*
* 출력 예시 : 3 4 4 3
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int m = scanner.nextInt();
        int [] arr = new int[n];
        for(int i=0; i<arr.length; i++){
            arr[i] = scanner.nextInt();
        }

        for(int x : solution(n, m, arr)){
            System.out.print(x + " ");
        }
    }

    public static List<Integer> solution(int n, int m, int [] arr){
        List<Integer> answer = new ArrayList<>();
        Map<Integer, Integer> map = new HashMap<>();

        for(int i=0; i< m-1; i++){
            map.put(arr[i], map.getOrDefault(arr[i], 0 ) + 1);
        }

        int left = 0;
        for(int right = m-1; right<n; right++){
            map.put(arr[right], map.getOrDefault(arr[right], 0) + 1);
            answer.add(map.size());

            map.put(arr[left], map.get(arr[left]) - 1);
            if(map.get(arr[left]) == 0){
                map.remove(arr[left]);
            }
            left++;
        }
        return answer;
    }
}
```

- 풀이

---

### 4. 모든 아나그램 찾기

설명

S문자열에서 T문자열과 아나그램이 되는 S의 부분문자열의 개수를 구하는 프로그램을 작성하세요.

아나그램 판별시 대소문자가 구분됩니다. 부분문자열은 연속된 문자열이어야 합니다.

입력

첫 줄에 첫 번째 S문자열이 입력되고, 두 번째 줄에 T문자열이 입력됩니다.

S문자열의 길이는 10,000을 넘지 않으며, T문자열은 S문자열보다 길이가 작거나 같습니다.

출력

S단어에 T문자열과 아나그램이 되는 부분문자열의 개수를 출력합니다.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
bacaAacba
abc
* 출력 예시 :3
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        String str1 = scanner.next();
        String str2 = scanner.next();
        System.out.println(solution(str1, str2));

    }

    public static int solution(String str1, String str2){
      int answer = 0;
      HashMap<Character, Integer> am = new HashMap<>();
      HashMap<Character, Integer> bm = new HashMap<>();

      //bm 미리 셋팅
      for(char x : str2.toCharArray()){
          bm.put(x , bm.getOrDefault(x , 0) + 1);
      }
      //am 미리 셋팅
      int length = str2.length() - 1; //2
      for(int i =0; i<length; i++){
          am.put(str1.charAt(i), am.getOrDefault(str1.charAt(i), 0) + 1);
      }

      //투포인트 알고리즘
      int lt= 0;
      for(int rt=length; rt<str1.length(); rt++){
          am.put(str1.charAt(rt), am.getOrDefault(str1.charAt(rt) , 0) + 1);
          if(am.equals(bm)){
              answer++;
          }
          am.put(str1.charAt(lt), am.get( str1.charAt(lt)) - 1);

          if(am.get(str1.charAt(lt)) == 0){
              am.remove(str1.charAt(lt));
          }
          lt++;
      }

      return answer;
    }
}
```

- 풀이
    
    해시맵 두개 am / bm 에 받은 시그니처 셋팅 → 투포인트 알고리즘 통해서 일치할시 answer ++ → lt 는 빼준후 put →
    
    0 인값이 있으면 remove 처리 → lt ++ → return;
    

---

### 5. K번째 큰수(TreeSet)

설명

현수는 1부터 100사이의 자연수가 적힌 N장의 카드를 가지고 있습니다. 같은 숫자의 카드가 여러장 있을 수 있습니다.

현수는 이 중 3장을 뽑아 각 카드에 적힌 수를 합한 값을 기록하려고 합니다. 3장을 뽑을 수 있는 모든 경우를 기록합니다.

기록한 값 중 K번째로 큰 수를 출력하는 프로그램을 작성하세요.

만약 큰 수부터 만들어진 수가 25 25 23 23 22 20 19......이고 K값이 3이라면 K번째 큰 값은 22입니다.

입력

첫 줄에 자연수 N(3<=N<=100)과 K(1<=K<=50) 입력되고, 그 다음 줄에 N개의 카드값이 입력된다.

출력

첫 줄에 K번째 수를 출력합니다. K번째 수가 존재하지 않으면 -1를 출력합니다.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
10 3
13 15 34 23 45 65 33 11 26 42

* 출력 예시 :143
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int m = scanner.nextInt();
        int [] arr = new int[n];
        for(int i=0; i<arr.length; i++){
            arr[i] = scanner.nextInt();
        }
        System.out.println(solution(n, m, arr));

    }

    public static int solution(int n, int m, int [] arr){
      int answer = -1;

      //중복제거 TreeSet 내림차순으로 정렬
      TreeSet<Integer> set = new TreeSet<>(Collections.reverseOrder());

        //3장을 뽑아 더하는 3중 포문
        for(int i=0; i<n; i++){
            for(int j=i+1; j<n; j++){
                for(int l=j+1; l<n; l++){
                    set.add(arr[i]+ arr[j]+arr[l]);
                }
            }
        }

        //for 문으로 돌려서 cnt 와 받은 시그니처(m) 의 자리가 똑같으면
        int cnt =0;
        for(int x: set){
            cnt ++;
            if(cnt == m){
                answer= x;
                break;
            }
        }

        return answer;
    }
}
```

---
