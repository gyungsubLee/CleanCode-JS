# 42 - Computed Property Name

JavaScript를 사용함에 있어서 react, vue의 문법적인 구분에서 헷갈려 실수를 한다.

그 중에 하나로 Computed Property Name이 있다.

Computed Property Name은 대괄호(`[]`)로 property를 감싸는 것이며, JavaScript의 `property`를 `동적`으로 다룰 수 있게 한다.(계산된 값이 들어옴.)

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

![image](https://user-images.githubusercontent.com/95308384/199219957-22dd431c-dff8-458c-ac90-b2b70d2a3a1f.png)

위 그림과 같이 `Computed property name([])`을 사용하여 동적으로 계산된 값을 속성으로 다를 수 있다.

<br/><br/>

## case2 - redux / handle actioins

```javascript
const noop = createAction("INCREMENT");

const reducer = handleActions(
  {
    [noop]: (state, action) => ({
      counter: state.counter + action.payload,
    }),
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
    //    함수명    / 매개변수 / 함수 Body
    [SOME_MUTATION](state) {},
  },
});
```

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
```

<br/>
<br/>

## 정리)

● Computed property name
property를 동적으로 할당 가능하게 한다.

> 확실하게 정리 안됨... -> 복습하면서 이해될 때 다시 정리
