## 1. 선택정렬(On2)

설명

N개이 숫자가 입력되면 오름차순으로 정렬하여 출력하는 프로그램을 작성하세요.

정렬하는 방법은 선택정렬입니다.

입력
첫 번째 줄에 자연수 N(1<=N<=100)이 주어집니다.

두 번째 줄에 N개의 자연수가 공백을 사이에 두고 입력됩니다. 각 자연수는 정수형 범위 안에 있습니다.

출력
오름차순으로 정렬된 수열을 출력합니다.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
6
13 5 11 7 23 15

* 출력 예시 : 5 7 11 13 15 23
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int [] arr = new int[n];

        for(int i=0; i<n; i++){
            arr[i] = scanner.nextInt();
        }

        for(int i : solution(n, arr)){
            System.out.print(i + " ");
        }
    }

    public static int[] solution(int n, int [] arr){
        for(int i=0; i<n - 1; i++){ // n - 1 : 마지막 앞까지만 찾으면 됨 마지막은 찾을필요X 
            int min = i;
            for(int j=i + 1; j < n; j++){
                if(arr[min] > arr[j]){
                    min = j; //j 로 교체. -> 가장 작은숫자의 인덱스 번호를 저장
                }
            }
            swap(arr, min, i); //교체작업
        }

        return arr;
    }

    static void swap(int[] a, int idx1, int idx2) {
        int temp = a[idx1];  
				a[idx1] = a[idx2];  
				a[idx2] = temp;
    }
}
```

- 풀이

이중 for 문을 돌면서 j 는 배열 1부터 돈다 → if 문에서 min 에 j 인덱스를 저장하여 → 그후에 swap 처리 → 오름차순으로 정렬 → return;

- min 은 해당 인덱스 값으로 고정하면서 계속 for 문을 돈다

---

## 2. 버블정렬(On2)

설명

N개이 숫자가 입력되면 오름차순으로 정렬하여 출력하는 프로그램을 작성하세요.

정렬하는 방법은 버블정렬입니다.

입력

첫 번째 줄에 자연수 N(1<=N<=100)이 주어집니다.

두 번째 줄에 N개의 자연수가 공백을 사이에 두고 입력됩니다. 각 자연수는 정수형 범위 안에 있습니다.

출력

오름차순으로 정렬된 수열을 출력합니다.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
6
13 5 11 7 23 15

* 출력 예시 : 5 7 11 13 15 23
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int [] arr = new int[n];

        for(int i=0; i<n; i++){
            arr[i] = scanner.nextInt();
        }

        for(int i : solution(n, arr)){
            System.out.print(i + " ");
        }
    }

    public static int[] solution(int n, int [] arr){
        for(int i=0; i<n - 1; i++){
            for(int j=n-1; j>i; j--){
                if(arr[j-1] > arr[j]){
                    swap(arr, j-1 ,j);
                }
            }
        }
        return arr;
    }

    static void swap(int[] a, int idx1, int idx2) {
        int temp = a[idx1];
        a[idx1] = a[idx2];
        a[idx2] = temp;
    }
}
```

- 풀이
    
    한번의 패스에서 j 의 값이  i + 1 이 될때까지 비교, 교환을 수행한다 그리고 비교하는 두 요소중 오른쪽 요소는 인덱스의 i + 1이 될 때까지 감소하고 왼쪽 요소의 인덱스는 i 가 될 때까지 감소합니다. 서로 한 칸 이상 떨어져 있는 요소를 교환 하는 것이 아니라 서로 이웃한 요소에 대해서만 교환하므로 이 정렬 알고리즘은 안정적이라고 할 수 있음. 첫 번째 패스는 n -1 회, 두번째 패스는 n - 2 회.. 이런식으로 배열 뒤에서부터 정렬.
    

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
6
13 5 11 7 23 15

* 출력 예시 : 5 7 11 13 15 23
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int [] arr = new int[n];

        for(int i=0; i<n; i++){
            arr[i] = scanner.nextInt();
        }

        for(int i : solution(n, arr)){
            System.out.print(i + " ");
        }
    }

    public static int[] solution(int n, int [] arr){
        for(int i=0; i<n-1; i++){
            for(int j=0; j<n-i-1; j++){
                if(arr[j]>arr[j+1]){
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }

        return arr;
    }
}
```

---

## **3. 삽입 정렬**

설명

N개이 숫자가 입력되면 오름차순으로 정렬하여 출력하는 프로그램을 작성하세요.

정렬하는 방법은 삽입정렬입니다.

입력

첫 번째 줄에 자연수 N(1<=N<=100)이 주어집니다.

두 번째 줄에 N개의 자연수가 공백을 사이에 두고 입력됩니다. 각 자연수는 정수형 범위 안에 있습니다.

출력

오름차순으로 정렬된 수열을 출력합니다.

1. 예시1(내풀이)

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
6
11 7 5 6 10 9

* 출력 예시 : 5 6 7 9 10 11
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int [] arr = new int[n];

        for(int i=0; i<n; i++){
            arr[i] = scanner.nextInt();
        }

        for(int i : solution(n, arr)){
            System.out.print(i + " ");
        }
    }

    public static int[] solution(int n, int [] arr){

        for(int i=1; i<arr.length; i++){
            int temp = arr[i];
            for(int j=i-1; j>=0; j--){
                if(arr[j] > temp){ // temp 보다 값이 작으면
                    arr[j + 1] = arr[j]; //값을 뒤로 미뤄준다.
                    arr[j] = temp;
                }else{
                    break;
                }
            }
        }

        return arr;
    }
}
```

1. 예시2

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
6
11 7 5 6 10 9

* 출력 예시 : 5 6 7 9 10 11
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int [] arr = new int[n];

        for(int i=0; i<n; i++){
            arr[i] = scanner.nextInt();
        }

        for(int i : solution(n, arr)){
            System.out.print(i + " ");
        }
    }

    public static int[] solution(int n, int [] arr){

        for(int i=1; i<arr.length; i++){
            int temp = arr[i], j;
            for(j=i-1; j>=0; j--){
                if(arr[j] > temp){ // temp 보다 값이 작으면
                    arr[j + 1] = arr[j]; //값을 뒤로 미뤄준다.
                }else{
                    break;
                }
            }
            arr[j] = temp;
        }

        return arr;
    }
}
```

---

## **4. Least Recently Used**

설명

캐시메모리는 CPU와 주기억장치(DRAM) 사이의 고속의 임시 메모리로서 CPU가 처리할 작업을 저장해 놓았다가

필요할 바로 사용해서 처리속도를 높이는 장치이다. 워낙 비싸고 용량이 작아 효율적으로 사용해야 한다.

철수의 컴퓨터는 캐시메모리 사용 규칙이 LRU 알고리즘을 따른다.

LRU 알고리즘은 Least Recently Used 의 약자로 직역하자면 가장 최근에 사용되지 않은 것 정도의 의미를 가지고 있습니다.

캐시에서 작업을 제거할 때 가장 오랫동안 사용하지 않은 것을 제거하겠다는 알고리즘입니다.

![https://cote.inflearn.com/public/upload/c366c701c2.jpg](https://cote.inflearn.com/public/upload/c366c701c2.jpg)

캐시의 크기가 주어지고, 캐시가 비어있는 상태에서 N개의 작업을 CPU가 차례로 처리한다면 N개의 작업을 처리한 후

캐시메모리의 상태를 가장 최근 사용된 작업부터 차례대로 출력하는 프로그램을 작성하세요.

입력

첫 번째 줄에 캐시의 크기인 S(3<=S<=10)와 작업의 개수 N(5<=N<=1,000)이 입력된다.

두 번째 줄에 N개의 작업번호가 처리순으로 주어진다. 작업번호는 1 ~100 이다.

출력

마지막 작업 후 캐시메모리의 상태를 가장 최근 사용된 작업부터 차례로 출력합니다.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
5 9
1 2 3 2 6 2 3 5 7

* 출력 예시 : 7 5 3 2 6
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int m = scanner.nextInt();
        int [] arr = new int[m];

        for(int i=0; i<m; i++){
            arr[i] = scanner.nextInt();
        }

        for(int i : solution(n, m, arr)){
            System.out.print(i + " ");
        }
    }

    public static int[] solution(int size, int m, int [] arr){
        int [] cache = new int[size];

        for(int x : arr){
            int pos=-1;
            //캐시에 최근 작업이 이미 있다면? 최근작업 시기를 pos 에 저장.
            for(int i=0; i<size; i++) if(x == cache[i]) pos=i;

            if(pos==-1){ //캐시에 최근 작업이 없다면?
                for(int i=size-1; i>=1; i--){
                    cache[i] = cache[i -1];
                } //전체 캐시를 한칸씩 뒤로 옮긴다.
            }else{ //캐시에 최근 작업이 이미 있다면?
                for(int i=pos; i>=1; i--){ //최근 작업이 있던 위치까지 한칸씩 뒤로 옮긴다.
                    cache[i] = cache[i -1];
                }
            }
            cache[0]=x; //최근 작업을 맨 앞에 넣는다.
        }

        return cache;
    }
}
```

---

## **5. 중복 확인**

설명

현수네 반에는 N명의 학생들이 있습니다.

선생님은 반 학생들에게 1부터 10,000,000까지의 자연수 중에서 각자가 좋아하는 숫자 하나 적어 내라고 했습니다.

만약 N명의 학생들이 적어낸 숫자 중 중복된 숫자가 존재하면 D(duplication)를 출력하고,

N명이 모두 각자 다른 숫자를 적어냈다면 U(unique)를 출력하는 프로그램을 작성하세요.

입력

첫 번째 줄에 자연수 N(5<=N<=100,000)이 주어진다.

두 번째 줄에 학생들이 적어 낸 N개의 자연수가 입력된다.

출력

첫 번째 줄에 D 또는 U를 출력한다.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
8
20 25 52 30 39 33 43 33

* 출력 예시 : D
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int [] arr = new int[n];

        for(int i=0; i<n; i++){
            arr[i] = scanner.nextInt();
        }

        System.out.println(solution(n, arr));
    }

    public static String solution(int size, int [] arr){
        String answer = "U";

        Arrays.sort(arr);
        for(int i=0; i<size-1; i++){
            if(arr[i] == arr[i + 1]) return "D";
        }

        return answer;
    }
}
```

## **6. 장난꾸러기**

설명

새 학기가 시작되었습니다. 철수는 새 짝꿍을 만나 너무 신이 났습니다.

철수네 반에는 N명의 학생들이 있습니다.

선생님은 반 학생들에게 반 번호를 정해 주기 위해 운동장에 반 학생들을 키가 가장 작은 학생부터 일렬로 키순으로 세웠습니다.

제일 앞에 가장 작은 학생부터 반 번호를 1번부터 N번까지 부여합니다. 철수는 짝꿍보다 키가 큽니다.

그런데 철수가 앞 번호를 받고 싶어 짝꿍과 자리를 바꿨습니다.

선생님은 이 사실을 모르고 학생들에게 서있는 순서대로 번호를 부여했습니다.

철수와 짝꿍이 자리를 바꾼 반 학생들의 일렬로 서있는 키 정보가 주어질 때 철수가 받은 번호와 철수 짝꿍이 받은 번호를

차례로 출력하는 프로그램을 작성하세요.

입력

첫 번째 줄에 자연수 N(5<=N<=100)이 주어진다.

두 번째 줄에 제일 앞에부터 일렬로 서있는 학생들의 키가 주어진다.

키(높이) 값 H는 (120<=H<=180)의 자연수 입니다.

출력

첫 번째 줄에 철수의 반 번호와 짝꿍의 반 번호를 차례로 출력합니다.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
9
120 125 152 130 135 135 143 127 160

* 출력 예시 : 3 8
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int [] arr = new int[n];

        for(int i=0; i<n; i++){
            arr[i] = scanner.nextInt();
        }

        for(int i : solution(n, arr)){
            System.out.print(i + " ");
        }
    }

    public static List<Integer> solution(int size, int [] arr){
        List<Integer> answer = new ArrayList<>();
        int [] temp = arr.clone();

        for(int i=0; i<size; i++){
            if(arr[i] != temp[i]){
                answer.add(i + 1);
            }
        }

        return answer;
    }
}
```

## **7. 좌표 정렬(compareTo)**

설명

N개의 평면상의 좌표(x, y)가 주어지면 모든 좌표를 오름차순으로 정렬하는 프로그램을 작성하세요.

정렬기준은 먼저 x값의 의해서 정렬하고, x값이 같을 경우 y값에 의해 정렬합니다.

입력

첫째 줄에 좌표의 개수인 N(3<=N<=100,000)이 주어집니다.

두 번째 줄부터 N개의 좌표가 x, y 순으로 주어집니다. x, y값은 양수만 입력됩니다.

출력

N개의 좌표를 정렬하여 출력하세요.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
5
2 7
1 3
1 2
2 5
3 6

* 출력 예시 :
1 2
1 3
2 5
2 7
3 6
* */

class Point implements Comparable<Point>{
    public int x, y;
    Point(int x, int y){
        this.x = x;
        this.y = y;
    }
    @Override
    public int compareTo(Point o){
        //음수가 리턴되도록 해야함.
        if(this.x == o.x){
            return this.y - o.y;
        }else{
            return this.x - o.x;
        }
    }
}

public class Main {
    public static void main(String[] args) {

       Scanner scanner = new Scanner(System.in);
       int n = scanner.nextInt();
       ArrayList<Point> points = new ArrayList<>();

       for(int i=0; i<n; i++){
           int x = scanner.nextInt();
           int y = scanner.nextInt();
           points.add(new Point(x, y)); //리스트에 추가
       }
       //Comparable 인터페이스를 통해서 포인터 클래스에서 오버라이딩한 compareTo 정렬 기준으로 정렬해준다
       Collections.sort(points);
        for(Point o : points){
            System.out.println(o.x + " " + o.y);
        }
    }
}
```

- 보충설명

### compareTo의 정렬 기준

1. **compareTo의 리턴 결과가 양수**
    - `compareTo` 메서드를 부르는 객체가 더 크고, 파라미터로 들어온 Point 의 o 객체가 더 작다고 판별된다.
    - 주체객체와 대상객체가 교체하여 정렬된다.
2. **compareTo의 리턴 결과가 0**
    - 두 객체의 값이 동일하다고 판별된다.
    - 정렬을 유지한다.
3. **compareTo의 리턴 결과가 음수**
    - `compareTo` 메서드를 부르는 객체가 더 작고, 파라미터로 들어온 Point 의 o 객체가 더 크다고 판별된다.
    

위 예시에서는 좌표값 x 가 동일할시에 y 값이 오름차순으로 정렬되고, 아닐시에는 좌표 x 값 기준으로 정렬됩니다

내림차순으로 정렬하고싶으면 this 값과 시그니처로 받은 Point 의 매개변수 o 를 바꿔줘야한다.

### Collection.sort(객체)

사용 시 대상 객체가 정렬된다. 그 기준은 위에서 `Comparable` 인터페이스로 정의한 기준에 따라 정렬된다. 기본 데이터형과 달리 객체의 경우 정렬 기준을 정의하지 않으면 컴파일 에러가 난다.

- 참고 링크

[https://www.daleseo.com/java-comparable-comparator/](https://www.daleseo.com/java-comparable-comparator/)

## **8. 이분검색**

설명

임의의 N개의 숫자가 입력으로 주어집니다. N개의 수를 오름차순으로 정렬한 다음 N개의 수 중 한 개의 수인 M이 주어지면

이분검색으로 M이 정렬된 상태에서 몇 번째에 있는지 구하는 프로그램을 작성하세요. 단 중복값은 존재하지 않습니다.

입력

첫 줄에 한 줄에 자연수 N(3<=N<=1,000,000)과 M이 주어집니다.

두 번째 줄에 N개의 수가 공백을 사이에 두고 주어집니다.

출력

첫 줄에 정렬 후 M의 값의 위치 번호를 출력한다.

1. 내 풀이

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
8 32
23 87 65 12 57 32 99 81

* 출력 예시 : 3
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int m = scanner.nextInt();
        int [] arr = new int[n];

        for(int i=0; i<n; i++){
            arr[i] = scanner.nextInt();
        }

        System.out.println(solution(n, m, arr));

    }

    public static int solution(int n, int m, int [] arr){
        int answer = 0;

        Arrays.sort(arr);
        for(int i=0; i<arr.length; i++){
            if(arr[i] == m){
                answer = i + 1;
            }
        }
        return answer;
    }
}
```

- 풀이

그냥 분기처리해서 쉽게 풀었지만 이분검색으로 풀어야하니까 문제 의도와는 맞지는 않는듯? → 위에건 순차검색임

1. 예시2

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
8 32
23 87 65 12 57 32 99 81

* 출력 예시 : 3
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int m = scanner.nextInt();
        int [] arr = new int[n];

        for(int i=0; i<n; i++){
            arr[i] = scanner.nextInt();
        }

        System.out.println(solution(n, m, arr));

    }

    public static int solution(int n, int m, int [] arr){
        int answer = 0;

        Arrays.sort(arr);
        int lt = 0;
        int rt = n - 1;
        //이분검색
        while (lt<=rt){
            int mid = (lt + rt) / 2;
            if(arr[mid] == m){
                answer = mid + 1;
                break; //while 문 종료
            }
            //찾고자 하는 값보다 클경우? -> 그 index 부분은 검색할 필요가 없으므로
            //범위를 좁혀야한다.
            if(arr[mid] > m){
                rt = mid - 1; //rt 범위 축소
            }else{
                lt = mid + 1; //lt 범위 축소
            }
        }

        return answer;
    }
}
```

- 풀이

시간 복잡도는 O(log2N) 으로 찾고자하는 숫자를 기준으로 배열부분의 범위를 좁혀가면서 검색해야한다.

## **9. 뮤직비디오(결정알고리즘)**

설명

지니레코드에서는 불세출의 가수 조영필의 라이브 동영상을 DVD로 만들어 판매하려 한다.

DVD에는 총 N개의 곡이 들어가는데, DVD에 녹화할 때에는 라이브에서의 순서가 그대로 유지되어야 한다.

순서가 바뀌는 것을 우리의 가수 조영필씨가 매우 싫어한다. 즉, 1번 노래와 5번 노래를 같은 DVD에 녹화하기 위해서는

1번과 5번 사이의 모든 노래도 같은 DVD에 녹화해야 한다. 또한 한 노래를 쪼개서 두 개의 DVD에 녹화하면 안된다.

지니레코드 입장에서는 이 DVD가 팔릴 것인지 확신할 수 없기 때문에 이 사업에 낭비되는 DVD를 가급적 줄이려고 한다.

고민 끝에 지니레코드는 M개의 DVD에 모든 동영상을 녹화하기로 하였다. 이 때 DVD의 크기(녹화 가능한 길이)를 최소로 하려고 한다.

그리고 M개의 DVD는 모두 같은 크기여야 제조원가가 적게 들기 때문에 꼭 같은 크기로 해야 한다.

입력

첫째 줄에 자연수 N(1≤N≤1,000), M(1≤M≤N)이 주어진다.

다음 줄에는 조영필이 라이브에서 부른 순서대로 부른 곡의 길이가 분 단위로(자연수) 주어진다.

부른 곡의 길이는 10,000분을 넘지 않는다고 가정하자.

출력

첫 번째 줄부터 DVD의 최소 용량 크기를 출력하세요.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
9 3
1 2 3 4 5 6 7 8 9

* 출력 예시 : 17
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int m = scanner.nextInt();
        int [] arr = new int[n];

        for(int i=0; i<n; i++){
            arr[i] = scanner.nextInt();
        }
        System.out.println(solution(n, m, arr));
    }

    public static int solution(int n, int m, int[] arr){
        int answer = 0;
        int lt = Arrays.stream(arr).max().getAsInt(); //배열 반복자 stream 을 통한 arr 의 최대값
        int rt = Arrays.stream(arr).sum();            //배열 반복자 stream 을 통한 arr 의 합

        while(lt<=rt){
            int mid = (lt + rt)/2;
            if(count(arr, mid) <= m){
                answer = mid;
                rt = mid -1;
            }else {
                lt = mid +1;
            }
        }
        return answer;
    }

    // 해당 용량(capacity)에 필요한 DVD 개수 return
    // 리턴값이 m보다 같거나 작은 경우만 해당 용량이 문제의 조건을 만족
    public static int count(int[] arr, int capacity){
        int cnt = 1; //DVD 장 수
        int sum = 0; //DVD 에 담아내는 곡들의 합
        for(int x : arr){
            // sum + x : cnt = 1이므로 첫번째 DVD에 곡을 '담아보는' 것 부터 시작하기
            if(sum + x > capacity){
                cnt++;   //새로운 DVD 준비
                sum = x; //새로운 DVD 장으로 초기화
            }else{
                sum+= x;
            }
        }
        return cnt;
    }
}
```

- 풀이
    
    ## 전략
    
    - 이분검색을 이용하는 알고리즘
    - 특정 범위 (lt ~ rt) 사이에 답(최소 용량)이 있다는 확신이 있는 경우에만 적용 가능한 알고리즘
        
        > lt ~ rt
        a. lt 는 9
        아홉번째 노래가 가장 긴 9분짜리이기 때문에 DVD는 최소한 9분 이상의 용량이 되어야한다.
        b. rt 는 45
        DVD의 최소용량은 적어도 모든 노래 길이를 더한 45 이하 일 것이다. 용량이 45일 경우 DVD 1장에 모든 노래를 다 담을 수 있게되는데, 당연히 3장에도 담을 수 있으므로 조건을 만족함
        > 
    
    ### 동작원리
    
    1. 9(lt) / 27(mid) / 45(rt) mid값을 DVD 한 장의 용량이라고 가정하면 (123456)(789) 두 장에 담을 수 있으므로 당연히 3장에도 담을 수 있다.
        
        > -조건 만족하나 가장 최소 용량이 맞는지는 다음 단계에서 추가 확인-'최소'용량을 찾아야 하므로 28 ~ 45까지는 볼 필요가 없다
        > 
    2. 9(lt) / 17(mid) / 26(rt)mid값을 DVD 한 장의 용량이라고 가정하면 (12345)(67)(89) 3장에 담을 수 있다.
        
        > -조건 만족하나 가장 최소 용량이 맞는지는 다음 단계에서 추가 확인-1단계 보다 더 적은 용량이므로 더욱 최적해에 가까움
        > 
    3. 9(lt) / 12(mid) / 16(rt)mid값을 DVD 한 장의 용량이라고 가정하면 (1234)(56)(7)(8)(9) 다섯 장에 담을 수 있다. (조건불만족)
    4. 13(lt) / 14(mid) / 16(rt)...

## **10. 마구간 정하기(결정알고리즘)**

설명

N개의 마구간이 수직선상에 있습니다. 각 마구간은 x1, x2, x3, ......, xN의 좌표를 가지며, 마구간간에 좌표가 중복되는 일은 없습니다.

현수는 C마리의 말을 가지고 있는데, 이 말들은 서로 가까이 있는 것을 좋아하지 않습니다. 각 마구간에는 한 마리의 말만 넣을 수 있고,

가장 가까운 두 말의 거리가 최대가 되게 말을 마구간에 배치하고 싶습니다.

C마리의 말을 N개의 마구간에 배치했을 때 가장 가까운 두 말의 거리가 최대가 되는 그 최대값을 출력하는 프로그램을 작성하세요.

입력

첫 줄에 자연수 N(3<=N<=200,000)과 C(2<=C<=N)이 공백을 사이에 두고 주어집니다.

둘째 줄에 마구간의 좌표 xi(0<=xi<=1,000,000,000)가 차례로 주어집니다.

출력

첫 줄에 가장 가까운 두 말의 최대 거리를 출력하세요.

```java
package Main;

import java.util.*;

/*
* 입력 예시 :
5 3
1 2 8 4 9

* 출력 예시 : 3
* */
public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int m = scanner.nextInt();
        int [] arr = new int[n];

        for(int i=0; i<n; i++){
            arr[i] = scanner.nextInt();
        }
        System.out.println(solution(n, m, arr));
    }

    public static int solution(int n, int m, int[] arr){
        int answer = 0;
        Arrays.sort(arr);
        int lt= 1;
        int rt= arr[n-1];
        while (lt <= rt){
            int mid = (lt + rt ) / 2;
            if(count(arr, mid) >= m){
                answer= mid;
                lt= mid + 1;
            }else{
                rt= mid - 1;
            }
        }
        return answer;
    }

    public static int count(int[] arr, int dist){
        int cnt= 1; // 말의 마릿수
        int ep= arr[0];
        for(int i=1; i<arr.length; i++){
            if(arr[i]-ep >= dist){
                cnt++;
                ep= arr[i]; //ep 교체
            }
        }
        return cnt;
    }
}
```

## 전략

- 범위 정하기lt : 좌표2 - 좌표1 = 최소거리1(또는 그냥 최소거리를 1로 해도 된다. 어차피 이분검색이기 때문에 반씩 줄어들어 검색속도가 빨라 큰 차이가 없음)rt : 가장큰좌표9 - 가장작은좌표1 = 최대거리8(but, 굳이 이렇게까지 범위를 줄일 필요는 없고, 그냥 배열의 마지막 좌표9를 rt로 잡아도 된다. 어차피 이분검색이기 때문에 반씩 줄어들어 검색속도가 빨라 큰 차이가 없음)
- 해당 lt ~ rt 범위마다 mid값(=가장 가까운 두 말의 최대 거리라고 가정)을 구하면서 3마리가 배치 되는지 여부를 확인한다.(5마리 배치 가능해도 3마리는 당연히 배치 가능하다. 따라서 count가 3보다 크거나 같으면 된다)
- 매 범위마다 첫번째 말은 무조건 첫번째 좌표에 넣는게 최대거리에 유리
- mid가 2일때 1, 4, 8에 말을 배치 시킬 수 있는데, 최대거리가 2와 일치하지 않음> mid값이 유효할 뿐 답인것은 아니다. 다음 범위의 mid값에서 일치하는 최대거리가 나올 것
