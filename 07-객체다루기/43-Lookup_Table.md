# 43 - Lookup Table

![image](https://user-images.githubusercontent.com/95308384/199480157-e433528d-ab19-4d5a-9f20-0eb7d5f6231f.png)

`Lookup Table`은 배열 데이터 구조에서 `key`와 `value`로 관리된 배열이 나열된 형태를 말한다.

> 예시는 다 Object인데 왜 배열로 설명을 하는지...?

<br/>
<br/>

## Bad case1 - if문

```javascript
function getUserType(type) {
  if (type === "ADMIN") {
    return "관리자";
  } else if (type === "INSTRUCTOR") {
    return "강사";
  } else if (type === "STUDENT") {
    return "수강생";
  } else {
    return "해당 없음";
  }
}
```

production에서 실제 개발을 할때, 요구사항(조건)이 추가될 때마다 불필요한 코드가 늘어난다.

business 커지면서, 해당하는 로직(if문)이 늘어나면서 유지보수도 어려우며 명시적이지 않다.

<br/>
<br/>

## Case2 - switch/case문

```javascript
function getUserType(type) {
  switch (key) {
    case "ADMIN":
      return "관리자";
    case "INSTRUCTOR":
      return "강사";
    case "STUDENT":
      return "수강생";
    default:
      return "해당 없음";
  }
}
```

if문이 많을 시 switch/case문으로 리펙토링하는 것이 더 좋은 코드이다. 그러나 switch/case로 변경하여도 나열되면서 불필요한 코드들이 늘어나는 것은 동일하다.

<br/>
<br/>

## Best Case3 - Object `LookUp Table`

### ● Object LookUp Table

```javascript
function getUserType(type) {
  const USER_TYPE = {
    ADMIN: "관리자",
    INSTRUCTOR: "강사",
    STUDENT: "수강생",
  };

  return USER_TYPE[type] || "해당 없음"; // or단축평가(||) -> 예외처리
}
```

`상수` 와 `Computed Property Name`을 사용한 `LookUp Table`을 통해 `유지보수가 간편`하고 더 `명시적`인 코드로 작성 가능하다.

<br/>

### ● or단축평가(||) -> null병합연산자(??)

```javascript
function getUserType(type) {
  const USER_TYPE = {
    ADMIN: "관리자",
    INSTRUCTOR: "강사",
    STUDENT: "수강생",
  };

  return USER_TYPE[type] ?? "해당 없음"; // null병합연산자 -> null, undefinded 예외처리
}
```

or단축평가(||)를 `null병합연산자(??)`로 변경하여 `null, undefinded만 예외처리`

<br/>

### ● UNDEFINED Object 추가

```javascript
function getUserType(type) {
  const USER_TYPE = {
    ADMIN: "관리자",
    INSTRUCTOR: "강사",
    STUDENT: "수강생",
    UNDEFINED: "해당 없음",
  };

  return USER_TYPE[type] || USER_TYPE.UNDEFINED;
}
```

위와 같이 `Object에 예외처리 로직을 추가`하면, 아래와 같이 `외부 모듈에서 해당 객체를 불`러올때 더 간편하게 로직을 작성할 수 있다.

```javascript
import USER_TYPE from "./constants/..some.js";

function getUserType(type) {
  return USER_TYPE[type] || USER_TYPE.UNDEFINED;
}
```

<br/>

### ● 바로 Object return

```javascript
function getUserType(type) {
  return (
    {
      ADMIN: "관리자",
      INSTRUCTOR: "강사",
      STUDENT: "수강생",
    }[type] ?? "해당 없음"
  );
}
```

내부에 `지역변수를 만들지 않`고 `바로 return` 처리

<br/>

## 정리)

### `LookUp table`

if문 or switch/case문 -> `LookUp table`(Object + 상수(const) + computed property name)

Object 형태로 조건을 key, return 값을 value로 computed property name을 사용하여 획기적으로 로직을 줄일 수 있다.

`상수`를 사용하여 LookUp Table과 Object를 잘 엮어 사용하면 함수들을 더 유연하게 작성할 수 있다.

> JavaScript에서 상수(const)는 대문자로 작성한다.

<br/>

> 현업에서 많이 사용하니 `상수`와 `Object`를 엮어 `LookUp Table 잘 만`들어 사용할 수 있도록 숙지 필요
