# 52. Parameter & Argument

## Parameter

매개변수, Formal Parameter

```javascript
function axios(url) {
  // some code
}

// parameter: url
```

<br/>

### [나머지 매개변수(rest parameter)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/rest_parameters)

`spread` + prameter

함수가 `정해지지 않은 수의 매개변수`를 `배열`로 받을 수 있다.

```javascript
// 구문
function f(a, b, ...theArgs) {
  // ...
}
```

<br/>

```javascript
// 예시
function myFun(a, b, ...manyMoreArgs) {
  console.log("a", a);
  console.log("b", b);
  console.log("manyMoreArgs", manyMoreArgs);
}

myFun("one", "two", "three", "four", "five", "six");
// a, one
// b, two
// manyMoreArgs, [three, four, five, six]

myFun("one", "two", "three");
// a, "one"
// b, "two"
// manyMoreArgs, ["three"]
```

<br/>
<br/>

## Argument

인자, Actual Parameter

```javascript
axios("https://github.com");
]

// Argument: "https://github.com"
```

<br/>
<br/>

### [Arguments Object](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments)

`arguments 객체`는 함수에 전달된 인자에 해당하는 `Array 형태의 객체`이다.

`모든 함수 내`에서 이용 가능한 `지역 변수`이며, arguments 객체를 사용하여 함수 내에서` 모든 인수를 참조` 할 수 있다.

```javascript
function func1(a, b, c) {
  console.log(arguments[0]);
  // expected output: 1

  console.log(arguments[1]);
  // expected output: 2

  console.log(arguments[2]);
  // expected output: 3
}

func1(1, 2, 3);
```

<br/>
<br/>

## 나머지 매개변수: 실제 배열, arguments: 유사 배열

```javascript
function sortRestArgs(...theArgs) {
  let sortedArgs = theArgs.sort();
  return sortedArgs;
}

console.log(sortRestArgs(5, 3, 7, 1)); // 1, 3, 5, 7

function sortArguments() {
  let sortedArgs = arguments.sort();
  return sortedArgs;
}

console.log(sortArguments(5, 3, 7, 1));
// TypeError 발생 (arguments.sort is not a function)
```

`나머지 매개변수`에서는 `Array 메서드를 사용`할 수 있지만, `arguments 객체`에서는 `사용할 수 없`다.(Array.from()으로 배열 변환 필요)

<br/>
<br/>

---

Reference)<br/>
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments<br/>
https://developer.mozilla.org/en-US/docs/Glossary/Parameter<br/>
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/rest_parameters<br/>
https://developer.ozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments<br/>
https://www.udemy.com/course/clean-code-js/learn/lecture/29946846#announcementsr<br/>
