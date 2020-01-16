---
title :  "[JavaScript] #1. Hoisting 이란?"
category :
  - development
tag :
  - hoistring
  - javaScript
sidebar_main : true
header:
  teaser : /assets/images/category/devel-js.jpg
  overlay_image : /assets/images/category/devel-js.jpg
---

## 자바스크립트 호이스팅(Hoisting)

### Hoist란?
hoist 라는 단어의 사전적 정의는 끌어올리기 라는 뜻이다.
자바스크립트에서 끌어올려지는 것은 변수이다.

### 모든 변수 선언은 호이스트된다.
호이스트란 변수의 정의가 그 범위에 따라 선언과 할당으로 분리되는 것을 의미한다.
즉, 변수가 함수 내에서 정의되었을 경우, 선언이 함수의 최상위로,
함수 바깥에서 정의되었을 경우, 전역 컨텍스트의 최상위로 변경이 된다.



> var 변수의 의도치 않은 현상  

아래 코드를 보겠습니다.
```javascript
if(true){
  var name = 'yuddomack';
}
console.log(name);
for(var i=0; i<5; i++){
  // do something
}
console.log(i);
```

일반적인 프로그래밍 언어에서 변수는 블록 스코프{ } 안에서 유효하기 때문에, 블록이 종료된 시점에서 console.log를 호출하면 정상적으로 동작하지 않을거라고 생각됩니다.

하지만 'yuddomack'과 '5'가 콘솔에 출력되는 것을 볼 수 있습니다.

이러한 현상은 var 변수가 호이스팅 되기 때문에 발생합니다.



> 호이스팅(Hoisting)  

호이스팅은 var을 통해 정의된 변수의 선언문을 유효 범위의 최상단으로 끌어올리는 행위를 말합니다.

'선언과 할당의 분리'라고 생각하면 기억하기 좋을 것 같습니다.

```javascript
// <개발자가 작성한 코드>
if(true){
  var name = 'yuddomack';
}
console.log(name);
```

위 코드는 호이스팅에 의해 아래와 같은 모양으로 바뀌게 됩니다.

```javascript
// <호이스팅으로 변환된 코드>
var name; // 선언
if(true){
  name = 'yuddomack'; // 할당
}
console.log(name);
```

var name = 'yuddomack'이라고 정의한 변수가 실제로는 선언(var name)과 할당(name = 'yuddomack')이 분리되는 것 입니다.

때문에 여전히 name이라는 변수를 사용할 수 있는 것 입니다.



> var의 유효범위  

호이스팅 시 선언문은 유효 범위의 최상단으로 올라간다고 했습니다.

자바스크립트의 var는 단순한 블록{ }이 아닌 함수 블록function{ } 안에서 유효합니다. 이를 var는 함수 스코프에서 유효하다 라고 합니다.

```javascript
// <개발자가 작성한 코드>
function ho1(){
  if(true){
    var name = 'yuddomack';
  }
  console.log(name);
}

function ho2(){
  for(var i=0; i<5; i++){
    // do something
  }
  console.log(i);
}

if(true){
  var score = 100;
}
console.log(score);
```

위 코드는 호이스팅에 의해 아래와 같은 모양으로 바뀌게 됩니다.

```javascript
// <호이스팅으로 변환된 코드>
var score; // 선언

function ho1(){
  var name; // 선언

  if(true){
    name = 'yuddomack'; // 할당
  }
  console.log(name);
}

function ho2(){
  var i; // 선언

  for(i=0; i<5; i++){ // 할당
    // do something
  }
  console.log(i);
}

if(true){
  score = 100; // 할당
}
console.log(score);
```

var는 함수 스코프에서 유효하기 때문에 호이스팅 시, 선언문은 글로벌 스코프가 아닌 유효범위(함수) 내부의 최상단에 위치하게 됩니다.

글로벌 스코프 또한 하나의 함수 스코프 처럼 동작하기 때문에 호이스팅이 일어납니다.



> 함수 호이스팅  

함수의 선언 역시 호이스팅의 대상입니다. 때문에 스코프 내에서 어떤 위치에서 함수 선언을 하든지 호출할 수 있습니다.

```javascript
// <개발자가 작성한 코드>
sayName();

function sayName(){
  console.log('yuddomack');
}
```

```javascript
// <호이스팅으로 변환된 코드>
function sayName(){
  console.log('yuddomack');
}

sayName();
```

함수 선언 역시 최상단으로 끌어올려지기 때문에 sayName()을 먼저 호출하고 함수 정의를 이후에 하여도 정상적으로 동작하게 됩니다.

그렇다면 아래의 경우는 어떨까요?

```javascript
// <개발자가 작성한 코드>
sayName();

var sayName = function(){
  console.log('yuddomack');
}
```

선언 방식이 약간 다르지만, 두 방식 모두 함수를 선언한 것 입니다.

function sayName(){}는 함수 선언식, var sayName = function(){}은 함수 표현식 이라고 합니다.

글을 계속 읽기 전에 잠시만 결과를 예상해 보실까요?


어떤 결과를 예상하셨을지 모르겠지만 에러가 발생하게 됩니다.
```javascript
// <호이스팅으로 변환된 코드>
var sayName;

sayName();

sayName = function(){
  console.log('yuddomack');
}
```

var sayName은 변수이기 때문이죠. 그렇기에 '선언과 할당'의 분리가 발생합니다. 

순서를 보자면 sayName이 선언되고 sayName()이 호출되지만 거기엔 아무것도 없습니다. 그 이후에 sayName에 함수가 정의되는 것이지요.



>  함수, 변수 우선순위   

지금까지 var 변수, 함수 선언식을 사용한 함수의 선언부가 유효범위의 최상단으로 호이스팅 된다는 것을 알아봤습니다.

그렇다면 호이스팅에서 변수가 우선일까요? 함수가 우선일까요?


변수 '할당'이 함수 선언보다 우선 순위이고, 함수 선언이 변수 선언보다 우선 순위입니다.

함수 선언문과 변수 할당문이 존재할경우, 변수 a선언 -> 함수 a선언 -> a에 값할당 순으로 실행되겠습니다.

```javascript
// <사용자가 작성한 코드>
var myName = "hi";

function myName() {
  console.log("yuddomack");
}
function yourName() {
  console.log("everyone");
}

var yourName = "bye";

console.log(typeof myName);
console.log(typeof yourName);
```

위 코드에서 콘솔에는 "function" 혹은 "string"이 나오게됩니다.

결과가 어떨지 예상되시나요?

```javascript
// <호이스팅으로 변환된 코드>
var myName;
var yourName;
function myName() {
  console.log("yuddomack");
}
function yourName() {
  console.log("everyone");
}

myName = "hi";
yourName = "bye";

console.log(typeof myName);
console.log(typeof yourName);
```


결과는 둘 다 "string"을 출력합니다.


호이스팅이 일어나면 실질적으로 위와 같은 순서로 실행되기 때문입니다.

변수가 선언되고, 함수가 할당되지만 다시 String 값이 들어가게 됩니다.