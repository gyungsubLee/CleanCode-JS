# Nullish coalescing operator(??)

Nullish coalescing operator(null 병합 연산자, ??)은 `null` 과 `undefined`를 `false` 평가하는 단축평가 연산자이다.

<br/>

## 예시1 - `||` -> `??`

```javascript
function createElement(type, height, width) {
  const element = document.createElement(type || "div");

  element.style.height = String(height || 10) + "px";
  element.style.width = String(width || 10) + "px";

  return element;
}

const el = createElement("div", 0, 0); // 0: Falsy

el.style.height; // '10px'
el.style.width; // '10px'
```

||(or 단축평가)의 경우 `Falsy인 0`을 `false`로 평가한다.

따라서 0으로 값을 설정하려는 경우 `|| -> ??`로 변경한다.

<br/>

```javascript
function createElement(type, height, width) {
  const element = document.createElement(type || "div");

  element.style.height = String(height ?? 10) + "px";
  element.style.width = String(width ?? 10) + "px";

  return element;
}

const el = createElement("div", 0, 0); // 0: Falsy

el.style.height; // '0px'
el.style.width; // '0px'
```

`null 병합 연산자(??, Nullish coalescing operator)`는 `null`과 `undefined`의 경우만을 `false`로 판단한다.

따라서 `0(Falsy)는 True로 평가`되어 정상적으로 출력된다.

<br/><br/>

## 예시2 - Ealry Return + ||, `??`

```javascript
function helloWorld(message) {
  if (!message) {
    return "Hello! World";
  }

  return "Hello! " + (message || "World");
}
```

위 코드에서 0(Falsy)인 경우를 출력하고 싶은 경우 `|| -> ??` 로 변경한다.

<br/>

```javascript
function helloWorld(message) {
  return "Hello! " + (message ?? "World");
}

helloWorld(0); // "Hello! 0 World"
```

`|| -> ??`로 변경<br/>
`null` 과 `undefined`를 제외한 경우를 true로 판단하여 0(Falsy)가 정상으로 출력됨.

<br/>

```javascript
function helloWorld(message) {
  if (!message) {
    return "Hello! World";
  }

  return "Hello! " + (message ?? "World");
}
```

Ealry Return을 사용하는 경우, Falsy의 경우 false로 평가된다. `null 병합 연산자(??)` 와 함께 사용하는 경우 조건 범위의 중복이 생겨, 오류가 발생할 수 있다.

(강의에선 ||(or단축평가)를 잘 몰라서 하는 실수라고 설명함.)

따라서 `Early Return의 경우`는 null 병합 연산자(??)가 아닌 `||(or단축평가)`를 사용해서 처리하는 것이 올바르다.

(default parameter를 사용하는 방법도 있으나, 해당 내용은 추후 함수 파트에서 다시 설명한다 하니 해당 강의 듣고 link를 추가하자)

<br/><br/>

## 예시3 - ||,&& + ??

```javascript
console.log(null || undefined ?? "foo") // SyntaxError

console.log((null || undefined) ?? "foo") // foo
```

`or연산자(||)`는 연산자 `우선순위 낮`기때문에 `괄호()`를 우선적으로 연산처리를 해야한다.

([연산자 우선순위 확인](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Operator_Precedence))

<br/>

```javascript
function getUserName(isLogin, user) {
  return isLogin && user ?? user.name;
}
```

<br/>
<br/>

## 정리)

`falsy`인 경우까지 포함하여 `true`로 평가하고 싶은 경우, ||(or단축평가)대신 `??(null병합연산자)`를 사용하자.

### ( ||,&& ) ?? <br/>

`||,&& 연산자`의 경우 연산자 `우선순위가 낮`아 ??와 함께 사용하는 경우 `괄호`로 우선적 연산처리가 필요하다.

<br/>

---

Reference)<br/>
https://www.udemy.com/course/clean-code-js/learn/lecture/29335882#announcements<br/>
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator#no_chaining_with_and_or_or_operators
