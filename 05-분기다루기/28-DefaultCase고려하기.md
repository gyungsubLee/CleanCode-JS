# Default Case 고려하기

유저에게서 데이터를 입력받는 경우 항상 올바른 형태의 데이터를 기대하기는 어렵다.

따라서 `잘못된 데이터가 들`어오는 경우, `error를 표시`해주거나 `default 값을 설정`하여 올바른 데이터를 넣어주는 처리를 해야한다.

<br/>

## 예시1 - `||(or)` -> default value 설정

```javascript
function sum(x, y) {
  x = x || 1;
  y = y || 1;
  return x + y;
}

sum(); // 2
```

<br/>

```javascript
function createElement(type, height, width) {
  const element = document.createElement(type || "div");

  element.style.height = height || 20;
  element.style.width = width || 20;

  return elements;
}

createElement();
```

팀의 코어 유틸리티 함수나 코어 라이브러리 함수를 개발하는 팀에서는 항상 입력값을 받지 못해 undefined일 때의 상황까지 염두해서 default value를 설정해야한다.

그러므로써 더욱 안전하고 확장성 높은 코드 작성이 기능하다.

<br/>
<br/>

## 예시2 - switch/case

```javascript
function registerDay(userInputDay) {
  switch (useInputDay) {
    case "월요일": // some code
    case "화요일": // some code
    case "수요일": // some code
    case "목요일": // some code
    case "금요일": // some code
    case "토요일": // some code
    case "일요일": // some code
    default:
      throw Error("입력값 존재 하지 않습니다.");
  }
}

e.target.value = "월ㄹ요일";
registerDay(e.target.value);
```

switch문에서 `default`키워드로 `default 값 설정`하여 해당하는 case가 없는 경우를 처리한다.

> switch문 / `default`: 매칭이 되는 케이스문이 없을때 실행되야 할 코드를 지정

<br/>
<br/>

## 예시3 - React/switch(switch문 아님)

```xml
const Root = () => {
    <Router history={browerHistory}>
        <Switch>
            <Route exact path="/" component={App}>
            <Route exact path="/" component={App}>
            <Route component={NotFound}> // 마지막 edge case 고려
        <Switch>
    </Route>
}
```

React에서 사용자가 잘못된 url로 접속 시, **default component** 설정(`<Route component={NotFound}>`)으로 `error표시`한다.

<br/>
<br/>

## 예시4 - 래핑

```javascript
function safeParseInt(number, radix) {
  return parseInt(number, radix || 10);
}
```

누군가 만든 코드도 `래핑`하여 `dafault case` 설정, -> **안전하게 코드 작성**

<br/>
<br/>

## 정리

프론트 엔드 개발자라면 `사용자의 실수를 예방`하기 위해 `default 값을 설정`하자.

1. ||(or단축평가)
2. switch/default
3. React/Default-components
4. 래핑
