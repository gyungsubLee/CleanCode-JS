# 58. Callback Function

자바스크립트에서 Callback Functio은 대부분 장풍을 유발하고 Promise와 asysn/await 바뀌는 비동기를 제어할 사용하는 기법으로만 많이 알고 있다.

> Callback 함수가 promise로 바꾸고? as 장풍 유발하는 안좋은 패턴이다?
>
> ### 🤔 장풍? 뭔소리임?
>
> <image src="https://user-images.githubusercontent.com/95308384/202702162-df88e74a-47f7-4efe-9736-6d93fa63adc1.png" width="50%">

> 콜백 지옥을 말하는 듯 하다. <br/>
> 출처 - https://bravenamme.github.io/2019/10/29/javascript-promise

<br/>

### 그러나 `Callback Function`은` 함수의 실행권(제어권)`을 `다른 함수로 위임`하는 것으로도 생각할 수 있다.

<br/>

## Case1 - `addEventListener`의 인자로 받는 Callback 함수의 제어권 위임

```javascript
someElement.addEventListener("click", function () {
  console.log(someElement + "클릭이 되었습니다.");
});
```

해당 element(someElement)에 addEventListener로 click evnet가 감지됐을 시, 인자로 받는 callback Fucntion을 실행하는 코드이다.

따라서 addEventListener의 click event 발생 시, `인자로 받는 callback 함수`는 `click을 발현시키는 브라우저의 사용자`에게 `제어권이 넘`어간다.

이것이 callback 함수의 제어권을 위임하는 하나의 사례이다.

<br/>

### 해당 사례 실제 구현

```javascript
// addEventListener 구현
DOM.prototype.addEventListener = function (eventType, cbFunc) {
  if (eventType === "click") {
    const clickEventObject = {
      target: {},
    };

    cbFunc(clickEventObject);
  }
};
```

해당 구현을 보면서 `무의식적으로 사용`했던 addEventListener의 `event 객체`를 해당 메소드(addEventListener)가 인자로 받아서 처리해준 것을 알 수 있다.

또한 addEventListener에서 callback을 받아와 실행시켜 `제어권이 넘`어가는 것도 확인할 수 있다.

<br/>
<br/>

## Case2 - 로그인 및 회원가입 확인 메세지

```javascript
function register() {
  const isConfirm = confirm("회원가입에 성공했습니다.");

  if (isConfirm) {
    redirectUserInfoPage();
  }
}

function login() {
  const isConfirm = confirm("로그인에 성공했습니다.");

  if (isConfirm) {
    redirectIndexPage();
  }
}
```

<br/>

### `callback 함수`로 `리펙토링`

```javascript
function confirmModeal(message, cbFunc = () => {Default 설정}) {
  const isConfirm = confirm(message);

  if (isConfirm && cbFunc) {
    cbFunc();
  }
}

function register() {
  confirmModeal("회원가입에 성공했습니다.", redirectUserInfoPage);
}

function login() {
  confirmModeal("로그인에 성공했습니다." , redirectUserInfoPage);
}
```

`중복되는 로직`을 `callback 함수`로 리펙토링하여 함수를 레이어를 나눠 유지보수 및 확장 측면에서도 효율적으로 개선할 수 있게 해준다.(함수형 프로그래밍 패러다임)

<br/>
<br/>

## 정리)

Callback 함수는 함수를 값으로써 다른 함수의 인자로 넘겨 제어권을 위임하는 것 이다.

함수형 프로그래밍

<br/>

---

reference)<br/>
https://www.udemy.com/course/clean-code-js/learn/lecture/29973748#announcements<br/>
