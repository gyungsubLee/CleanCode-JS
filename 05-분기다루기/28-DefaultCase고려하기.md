# Default Case 고려하기

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
      throw Error("입력값이 입력되지 않 았습니다.");
  }
}

e.target.value = "월ㄹ요일";
registerDay(e.target.value);
```

<br/>

## 예시3 - React/switch(switch문으로 변하진 않음.)

```javascript
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

<br/>

## 예시4 - 래핑, default case

```javascript
function safeParseInt(number, radix) {
  return parseInt(number, radix || 10);
}
```

누군가 만든 코드도 래핑하여 dafault case 설정, -> 안전하게 코드 작성

<br/>
<br/>

## 정리

프론트 엔드 개발자라면 사용자의 실수를 예방하기 위해 default 값을 설정하자.
