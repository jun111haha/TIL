# this
자바스크립트에서 this는 기본적으로 실행 컨텍스트가 생성될 때 함께 결정된다 실행 컨텍스트는 함수를 호출할 때 생성되므로, 바꿔 말하면 this는 함수를 호출할 때 결정된다고‘ 볼수있음. 
함수를 어떤 방식으로 호출하느냐에 따라 값이 달라지는 것입니다.

## 전역공간에서 this
전역공간에서 this 는 전역 객체를 가르킨다. 개념상 전역 컨텍스트를 생성하는 주체가 바로 전역객체이기 떄문에. 전역 객체는 JS 런타임 환경에 따라 다른 이름과 정보를
가지고 있음. 브라우저 환경에서 전역객체는 window 이고, node.js 환경에서는 global 이다.

- 전역공간에서 this(브라우저)
```javascript
console.log(this); // { alert: f(), atob: f(), blur: f(), btoa: f(), ... } 
console.log(window); // { alert: f(), atob: f(), blur: f(), btoa: f(), ... } 
console.log(this === window); // true
```

- 전역공간에서 this(node.js 환경)
```javascript
console.log(this); // { alert: f(), atob: f(), blur: f(), btoa: f(), ... } 
console.log(global); // { alert: f(), atob: f(), blur: f(), btoa: f(), ... } 
console.log(this === global); // true
```

## 변수의 this
```javascript
var a = 1; 
console.log(a); // 1
console.log(window.a); // 1
console.log(this.a); // 1
```
전역공간에서 선언한 변수 a 에 1을 할당했을 뿐인데 window.a 와 this.a 에 모두 1이 출력된다.   
전역공간에서 this 는 전역객체를 의미하므로 두 값이 같은값을 출력하는 것은 당연하지만 그 값이 왜 1일까??   
-> 자바스크립트의 모든 변수는 실을 특정 객체의 프로퍼티로 서 동작한다.   

사용자가 var 연산자를 이용해 변수를 선언하더라도 실제 JS 엔진은 어떤 특정 객체의 프로퍼티로 인식한다. 특정 객체란 바로 실행 컨텍스트의 LexicalEnvironment 이하 (L.E) 이다.   
실행컨텍스트는 변수를 수집해서 L.E 의 프로퍼티로 저장합니다. 어떤 변수를 호출하면 L.E 를 조회해서 일치하는 프로퍼티가 있을 경우 그 값을 반환한다.   
전역 컨텍스트의 경우 L.E 는 전역객체를 그대로 참조한다.   

**"전역변수를 선언하면 자바스크립트 엔진은 이를 전역객체의 프로퍼티로 할당한다."**   
그렇다면 window.a 와 this.a 가 1이 나오는 이유는 설명이된다. a를 직접 호출할 때도 1이 나오는 까닭은?   
-> 이는 변수 a에 접근하고자 하면 스코프 체인에서 a 를 검색하다가 가장 마지막에 도달하는 전역 스코프의 L.E 즉 전역객체에서 해당 프로퍼티 a를 발견해서 그 값을 반환하기 때문이다.   
단순하게 window. 가 생략이 된것이라고 여겨도 된다.

## 함수로서 호출, 메서드로서 호출
<img width="787" alt="스크린샷 2022-12-01 오후 2 52 58" src="https://user-images.githubusercontent.com/59434443/204976393-749e2e27-5935-4a2d-b766-196e77c9ec5f.png">

1번째 줄에서 func 라는 변수에 익명함수를 할당. 4번쨰 줄에서 func 를 호출했더니 this 로 전역객체 Window 가 출력된다.   
6번쨰 줄에서 obj라는 변수에 객체를 할당하는데, 그 객체의 method 프로퍼티에 앞에서 만든 func 함수를 할당. 이제 9번쨰 줄에서   
obj 의 method 를 호출했더니, 이번에는 this 가 obj 라고 한다.    
-> 함수앞에 점(.) 여부만으로 구분가능. 함수와 메서드 호출을 구분 할 수 있다.

## 메서드 내부에서의 this
<img width="794" alt="스크린샷 2022-12-01 오후 2 55 43" src="https://user-images.githubusercontent.com/59434443/204976733-937b62bc-234d-4fe3-a59d-b7bf004e4f5d.png">

this 에는 호출한 주체에 대한 정보가 담긴다. 어떤 함수를 메서드로서 호출하는 경우 호출 주체는 바로 함수명(프로퍼티명) 앞의 객체   
점 표기법의 경우 마지막 점 앞에 명시된 곧 this 가 된다.   





