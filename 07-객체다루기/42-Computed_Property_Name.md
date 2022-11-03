# 42 - Computed Property Name

JavaScript를 사용함에 있어서 react, vue의 문법적인 구분에서 헷갈려 실수를 한다.

그 중에 하나로 `Computed Property Name`이 있다.

<br/><br/>

## Computed Property name

Computed Property name은 Object의 `property`를 `동적`으로 `변수`처럼 사용 가능하게 한다.

<br/>

### ● ES6전, 동적 property name

```javascript
const key = "name";
const value = "Atta";

const user = {};
user[key] = value;

console.log(user.name); // Atta
```

`computed property name 나오기 전(ES6 전)`, 객체에서 `동적으로 property name`을 만들려면, 위 예시와 같이 `객체를 만`들고 `대괄호 표기법([])`을 사용하여 value를 할당 처리를 해야됐다.

<br/>

### ● computed property name

```javascript
const key = "name";
const value = "Atta";

const user = {
  [key]: value,
};

console.log(user.name); // Atta
```

그러나 ES6+ 부터는 `computed property name`을 사용하여 `동적 property`를 `객체 안`에서 간편하게 작성할 수 있게 되었다.

따라서 위 예시와 같이 객체의 `key`에 `대괄호 표기법([])`을 사용하여 `property`를 `변수`처럼 `동적으로 할당` 가능하다.

<br/>

### ● computed property name -> 재작성(rewritten)

```javascript
const key = "name";
const value = "Atta";

const user = {
  [key + "34"]: value,
};

console.log(user.name34); // Atta
```

따라서 위 에시와 같이 `재작성`되어도 정상적으로 출력된다.

<br/>

### ● Computed property name + `template literals(`${}`)`

```javascript
const key = "name";
const value = "Atta";

const user = {
  [`${key}34`]: value,
};

console.log(user.name34); // Atta
```

위 예시와 같이 `객체 리터럴`과 함께 사용 가능하다.

<br/>
<br/>

## case1 - React

```javascript
import React, { useState } from "react";

function SomeComponent() {
  const [state, setState] = useState({
    id: "",
    password: "",
  });

  const handleChange = (e) => {
    setState({
      [e.target.name]: e.target.value,
    });
  };

  return (
    <React.Fragment>
      <input value={state.id} onChange={handleChange} name="name" />
      <input value={state.password} onChange={handleChange} name="password" />
    </React.Fragment>
  );
}

export default SomeComponent;
```

<br/>

![image](https://user-images.githubusercontent.com/95308384/199219957-22dd431c-dff8-458c-ac90-b2b70d2a3a1f.png)

위 예시와 같이 `event argument`를 통해 해당 `DOM property에 접근`하여 `동적 할당` 처리

`Computed property name([])`을 사용하여 동적으로 계산된 값을 속성으로 다를 수 있다.

> 동적으로 계산된 값이 무엇인지 정확하게 이해가 안간다...

<br/><br/>

## case2 - redux / handle actioins

```javascript
const noop = createAction("INCREMENT");

const reducer = handleActions(
  {
    [noop]: (state, action) => ({
      counter: state.counter + action.payload,
    }),
    //  [noop] (state, action) ({
    //    ounter: state.counter + action.payload,
    //  }),
  },
  { counter: 0 }
);
```

<br/><br/>

## Case3 - Vue

```javascript
import Vuex from "vuex";
import { SOME_MUTATION } from "./mutation-types";

export const SOME_MUTATION = "SOME_MUTATION";

const store = new Vuex.Store({
  state: {
    // some code...
  },
  mutations: {
    // 함수명 / 매개변수 / 함수 Body <- 함수와 동일
    [SOME_MUTATION](state) {},
  },
});
```

`consise method( ': funtion' 제거)` + `computed property method([])`

따라서

`[ computed property method ]` `( parameter )` `{ function body }` -> `함수`와 동일하게 동작함

<br/><br/>

##

```javascript
const funcName0 = "func0";
const funcName1 = "func1";
const funcName2 = "func2";

const obj = {
  [funcName0]() {
    return "func0";
  },
  [funcName1]() {
    return "func1";
  },
  [funcName2]() {
    return "func2";
  },
};

for (let i = 0; i < 3; i++) {
  console.log(obj[`func${i}`]());
}
// func0  func1  func2
```

`consise method( ': funtion' 제거)` + `computed property method([])`

<br/>
<br/>

## 정리)

● Computed property name<br/>

ES6+ 부터 사용 가능한 문법으로 `동적 property(변수)`를 더 편리하게 객체 안에서 작성 가능하게 함.

<br/>

<br/>

---

Reference)<br/>
https://attacomsian.com/blog/javascript-computed-property-names<br/>
https://www.udemy.com/course/clean-code-js/learn/lecture/29755922#announcements
