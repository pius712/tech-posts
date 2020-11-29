# this keyword

아래의 코드를 돌리고 `foo.count`를 보면 결과는 어떻게 될까?  
0이 된다.  

```js
function foo(){
    this.count++;
}
foo.count = 0;

foo();
foo();

foo.count
>>> 0
```

this는 객체 자신을 가리키고, 함수도 자바스크립트에서는 객체이기 때문에 foo 함수를 가리키는 것이 아닌가? 

**우선, this는 자기 자신을 가리키는 것이 아니다.**

그리고 **this는 함수 자신의 렉시컬 스코프를 가리키는 것도 아니다.**
아래의 코드는 foo 함수의 lexical scope을 가리켜서 호출되는 것이 아니라, 그저 this가 global객체를 가리키기 때문에 성공한 것이다.

```js
function foo(){
    var a = 2;
    this.bar();
}

function bar(){
    console.log('hi');
}
```


## this의 생성

this는 언제 생성될까? 
this는 **런타임 함수 호출시**에 바인딩되어 함수 호출 당시의 상황에 따라 실행 콘텍스트가 만들어진다. 

호출부가 어떻게 구현되어 있는가에 따라서 this는 바인딩되는 대상이 달라지게 된다!


## this binding

우선적으로 내용을 요약하면, 아래에 우선순위에 따라 this 바인딩이 결정된다. 

1. 함수가 new keyword가 붙어서 호출
2. call() or apply()로 함수 호출
3. 암시적 바인딩
4. default 바인딩

### default 바인딩

아래의 코드는 default 바인딩의 예이다. default 바인딩이 될 경우에는 this는 전역 객체(window, strict 모드시 undefined 값)에 바인딩 된다. 

```js 
function foo(){
  console.log(this.a);
}
var a = "hello world"
foo();
>>> hello world
```

### 암시적 바인딩

암시적 바인딩의 경우에는 호출부에 객체가 있는지 확인하는 것이다.
즉, 호출부에 함수에 대한 컨텍스트 객체가 있으면 이 객체에 암시적 바인딩이 된다.

```js
function foo() {
  console.log(this.a);
}
var obj = {
  a: 'hello world',
  foo: foo
}
obj.foo();
>>> 'hello world'
```

암시적 바인딩을 할 때 주의할 점.

1. 바인딩 소실 
아래의 코드에서 `bar = boo.foo` 부분을 조심해야한다. 여기서 변수 bar는 boo.foo를 가지는 것이 아니라, 
foo 레퍼런스를 직접 가리키기 때문에, 암시적 바인딩이 되지 않는다. 이 경우는 default binding이 적용된다.

```js
function foo(){
  console.log(this.a);
}
var boo = {
  a: 'hello world',
  foo: foo,
}
var bar = boo.foo;
var a = "bye"
bar();
>>> bye
```

2. 콜백함수

```js
function foo(){
  console.log(this.a);
}
function bar(fn){
  fn();
}
var obj = {
  a: 'hello world',
  foo: foo
}
a = "bye"
bar(obj.foo); // foo 함수의 레퍼런스를 직접 매개변수 fn이 가지게 된다.
>>> bye
```

## 명시적 바인딩

`call()` or `apply()` 함수를 통해서 함수를 특정 객체에 직접 바인딩 해주는 것이다.

```js
function foo(){
  console.log(this.a);
}
var obj = {
  a: 'hello world'
}
foo.call(obj);
>>> hello world
```

## new Binding

생성자 함수에 new를 붙여서 실행하게 되면, 생성된 객체에 this가 바인딩 된다.

```js
function foo(a){
  this.a = a;
}
var bar = new foo('hello world');
console.log(this.a);
>>> hello world
```

## arrow function

화살표 함수에서 this는 lexical scope을 가지게 된다. 

리액트에서 class 컴포넌트에서 function 선언 대신에 화살표 함수를 사용하게 되었을 경우, 
이를 prop으로 넘겨도 function 내부의 this는 넘겨 받은 함수의 this가 아니라, 생성된 클래스를 가리키게 된다.

그 이유는 화살표 함수에서의 this는 lexical scope에 따라 바인딩이 되는데, 
클래스를 통해 객체가 생성되면서 내부의 화살표 함수가 해당 객체에 this 바인딩이 되기 때문이다.
