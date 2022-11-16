# 54. Default Value

함수 안전하게 사용하는 방법 중 하나는 `함수가 받는 매개변수에 기본 값을 설정`해 주는 것이다.

<br/>

## Case1 - 인자가 존재하지 않는 `매개변수`(=`undefined`)에 기본값 설정

![image](https://user-images.githubusercontent.com/95308384/202169411-e3841813-6b57-411f-a0d8-d2d25cbd041e.png)

위 코드 예시를 보면 `createCarousel()` 호출 시 인자가 존재하지 않아 `options이 undefined`가 된다. 따라서 undefined 상태인 인자(options)에 `. 연산자`를 사용하여 property 호출 시 해당 객체가 정의되지 않아 `Error(Cannot read properties of undefined)`가 발생한다.

<br/>

```javascript
function createCarousel(options) {
  options = options || {};
  var margin = options.margin || 0;
  var center = options.center || false;
  var navElement = options.navElement || "div";

  // ..some code
  return {
    margin,
    center,
    navElement,
  };
}

createCarousel(); // { margin: 0, center: false, navElement: 'div' }
```

이러한 `Error를 기본값(Default Value)`을 설정하여 해결 가능하다.

<br/>
<br/>

## Case2 - 지역 변수 -> 매개변수 내부

Case1 에서의 지역 변수로 처리한 인자를들, `구조분해할당` 과 [할당연산자(=) 사용한 기본값 설정(default parameter)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)을 통해 아래와 같이 단축해서 작성 가능하다.

```javascript
function createCarousel({
  margin = 0,
  center = false,
  navElement = "div",
} = {}) {
  // ..some code
  return {
    margin,
    center,
    navElement,
  };
}

createCarousel();
```

<br/>
<br/>

## Case3 - 인자 = undefined 시, `required` 함수를 사용한 `Error` 표출

```javascript
const required = (argName) => {
  throw new Error("required is " + argName);
};

function createCarousel({
  items = required("items"),
  margin = 0,
  center = false,
  navElement = "div",
} = {}) {
  // ... some code

  return {
    margin,
    center,
    navElement,
  };
}

console.log(
  createCarousel({
    margin: 10,
    center: true,
    navElement: "span",
  })
);
```

<br/>
<br/>

## 정리)

### 기본값(Default Value) 설정

● `or 단축평가(||)`<br/>
● `Nullish coalescing operator(??)`<br/>
● `Default parameters(=)`<br/>

<br/>

Case1 - 기본값({}) 설정을 통한 Error(Cannot read properties of undefined) 해결

Case2 - ES2015+, 구조분해할당, default parameters를 통한 refactoring

Case3 - 인자 = undefined 시, 유틸함수 `required`를 사용한 `Error 처리`

<br/>

---

Reference)<br/>
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters<br/>
https://www.udemy.com/course/clean-code-js/learn/lecture/29955634#learning-tools<br/>
