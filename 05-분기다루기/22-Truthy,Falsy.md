# Truthy, Falsy

`JavaScript`는 **조건절, 반복문** 등 `불리언 값이 필요한 곳에서 불리언 값`으로 `형 변환`이 일어난다.

간단한 `boolean` 평가가 필요할 때, 사용하면 좋다.

<br/>

## [Truthy(참 같은 값)](https://developer.mozilla.org/ko/docs/Glossary/Truthy)

참 같은 값(Truthy)인 값이란, boolean을 기대하는 문맥에서 `true`로 평가되는 값

### Truthy 예시

```javascript
    if (true)
    if ({})
    if ([])
    if (42)
    if ("0")
    if ("false")
    if (new Date())
    if (-42)
    if (12n)
    if (3.14)
    if (-3.14)
    if (Infinity)
    if (-Infinity)
```

<br/>

### 강의 Truthy 예시

```javascript
if ("string".length > 0) {
}

if (!isNaN(10)) {
}

if (boolean === true) {
}

// truthy 변경
if ("string".length) {
}

if (10) {
}

if (boolean) {
}
```

<br/>
<br/>

## [Falsy(거짓 같은 값)](https://developer.mozilla.org/ko/docs/Glossary/Falsy)

거짓 같은 값(Falsy, falsey) 값은 불리언 문맥에서 `false`로 평가되는 값

### Falsy 예시

```javascript
    if (false)
    if (null)
    if (undefined)
    if (0)
    if (-0)
    if (0n)
    if (NaN)
    if ("")
```

<br/>

### 강의 Falsy 예시

```javascript
function printName(name) {
  // 안전한 코드를 위해 undefined, null 두가지 비교 -> 코드 길어짐
  if (name === undefined || name === null) {
    return "사람이 없네요";
  }

  return "안녕하세요 " + name + "님";
}

// falsy -> undefined, null 해당됨.
function printName(name) {
  if (!name) {
    // name으로 간편하게 undefined, null 평가 가능
    return "사람이 없네요";
  }
  return "안녕하세요 " + name + "님";
}

console.log(printName(null)); // 사람이 없네요.
console.log(printName(undefined)); // 사람이 없네요.
```

<br/>
<br/>

## 정리

Truthy & Falsy
-> 철저한 검사가 필요한 경우가 아닌, 간단하게 평가하는 경우 유용하게 사용 가능

---

Reference)<br/>
https://developer.mozilla.org/ko/docs/Glossary/Truthy<br/>
https://developer.mozilla.org/ko/docs/Glossary/Falsy<br/>
https://www.udemy.com/course/clean-code-js/learn/lecture/29189288#overview
