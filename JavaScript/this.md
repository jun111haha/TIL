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
