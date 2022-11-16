# 56. Void & Return

Void 특성을 가진 특수한 함수가 존재한다. 따라서 return 시, `undefined`가 return 된다.

이러한 경우의 return 처리는 불필요한 로직임으로 지양해야 한다.

api 사용 시, 해당 `명세에 return 값이 표시`되어 있다. `명세(MDN)를 구글링`하여 보는 습관을 가지자.

<br/>

## Case1 - Void 함수들의 return 처리 -> undefined return

```javascript
function handleClick() {
  return setState(false); // undefined
}

function showAlert(message) {
  return alert(message); // undefined
}
```

```javascript
// return 값 생략됨.
function test(sum1, sum2) {
  const result = sum1 + sum2;
}

function testVoidFunc() {
  return test(1, 2); // undefined
}

testVoidFunc(); // undefined
```

void의 속성을 갖는 함수들을 return 처리 시, undefined가 반환된다.

<br/>
<br/>

## Case2 - 반환 값이 필요한 함수들

```javascript
function isAdult(age) {
  return age > 19;
}

function getUserName(name) {
  return "유저 " + name;
}
```

반환 값이 항상 있어야하는 경우는 위 예시 코드와 같이 `함수명`에서부터 추론이 가능하다. (함수명을 명시적으로 작성해야하는 이유)

<br/>
<br/>

## 정리)

`void의 함수들`에 `return 처리`를 하는 실수를 한다. (undefined 반환됨)

사용하는 `api의 명세(MDN) 확인` 후, 해당하는 실수를 방지하자.

<br/>

---

Reference)
https://www.udemy.com/course/clean-code-js/learn/lecture/29973984#learning-tools
