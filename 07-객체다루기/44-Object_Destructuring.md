# 44. Object Destructuring (객체 분해)

> Destructuring(분해), 구조 분해 할당(destructuring assignment)

<br/>

## Case1 - 강제된 매개변수의 순서

### ● 예시

```javascript
function Person(name, age, location) {
  this.name = name;
  this.age = age;
  this.location = location;
}

const poco = new Person("poco", 30, "korea");
```

위 예시의 `문제점` -> `강제된` 매개변수들의 `순서`

<br/>

### ● 개선 - `parameter 객체 구조 변경` -> `구조분해할당` 처리

```javascript
function Person({ name, age, location }) {
  this.name = name;
  this.age = age;
  this.location = location;
}

const poco = new Person({
  name: "poco",
  age: 30,
  location: "korea",
});
```

argument의 데이터 구조를 `객체`로 바꾼 후 `구조분해할당`을 통해` 각각 변수로 할당` 처리하여 `순서의 강제성을 없`앤다.

<br/><br/>

## Case2 - `required` / `optional` Parameter

가장 핵심적인 매개변수를 name이라 하였을 때, `required` / `optional` Parameter 작성 예시

<br/>

### ● 예시

```javascript
function Person(name, options) {
  this.name = name;
  this.age = options.age;
  this.location = options.location;
}
```

구조분해할당이 나오기`전`, 위 예시와 같이 첫번째 인자를 필수적으로 받고 그 외 인자를 옵션으로 처리할 때, o`ptions 데이터들을 객체에 담`고 `property를 불`러오는 형태로 작성하였다.

<br/>

### ● 개선 - 구조분해할당

```javascript
function Person(name, { age, location }) {
  this.name = name;
  this.age = age;
  this.location = location;
}

const pocoOptions = {
  age: 30,
  location: "korea",
};

const poco = new Person("poco", pocoOptions);
```

`객체 구조분해할당`을 통해 `명시적`으로 받아올 수 있다.

<br/>
<br/>

## case3 - 배열 구조분해할당 처리

### ● 예시

```javascript
const orders = ["First", "Second", "Third"];

// index를 사용한 처리
const st = orders[0];
const rd = orders[2];
```

<br/>

### ● 개선 - 구조분해할당(`배열`) 처리

```javascript
const orders = ["First", "Second", "Third"];

// 배열 -> 구조분해할당 처리, 순서 강제됨.
const [first, , third] = orders;

console.log(first); // "First"
console.log(third); // "Third"
```

배열 구조분해할당 시 `순서`가 강제된다.

따라서 `const [first, , third] = orders;` 와 같이 두번째 인자를 건너뛰고 세번째 인자 사용 시 공백처리를 하여 순서를 지켜서 사용해야 한다.

<br/>

### ● 개선 - 구조분해할당(`객체`) 처리

```javascript
const orders = ["First", "Second", "Third"];

// 객체 -> 구조분해할당 처리
const { 0: st2, 2: rd2 } = orders;

console.log(st2); // "First"
console.log(rd2); // "Third"
```

자바스크립트에서 `배열`은 `객체`이기때문에 위 예시와 같이 `객체로 구조분해할당 처리`하여 사용 가능하다.

배열의 `요소가 많`을 시 `간단하게 분리`하는데 사용하기 용이하다.

<br/><br/>

## case4 - React Props

### ● 예시

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(element, document.getElementById("root"));
```

<br/>

### ● 개선 - Props 구조분해할당 처리

```javascript
function Welcome({ name }) {
  return <h1>Hello, {name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(element, document.getElementById("root"));
```

위와 같이 `Props`를 `구조분해할당 처리`하여 `명시적`으로 코드 작성 가능하다.

<br/>
<br/>

## 정리)

구조분해할당을 통해 데이터를 `명시적`으로 처리해야한다.

배열 구조분해할당 : 순서 중요!

객체 구조분해할당

배열 -> 객체 구조분해할당 : 자바스크립트에서 배열 == 객체, 따라서 key(=index)로 처리 가능

props = 객체 -> 객체 구조분해할당 -> 명시적

> 자주쓰이는 문법이 확실히 인지하고 사용할 것
