# 41. Shorthand Properties

모던 자바스크립트(ES2015+) 부터

Object의 key와 value 명이 같을 시 `하나의 명으로 숏코딩(Shorthand Properties`) 가능,

`key, value 구분 없`이 method 선언 가능(`Concise Method`)

<br/>

## case1 - Object -> `Shorthand Properties`, `Concise Method` 리펙토링

```javascript
const person = {
    firstName = 'poco',
    lastName = 'jang',
    getFullName: () => {
        return this.firstName + ' ' + this.lastName;
    },
},
```

<br/>
<br/>

### `Shorthand Properties`, `Concise Method` 리펙토링

#### Shorthand Properties

```javascript
// ● Shorthand Properties
const firstName = "poco";
const lastName = "jang";

const person = {
  firstName,
  lastName,
  getFullName: function () {
    return this.firstName + " " + this.lastName;
  },
};
```

<br/>

Concise Method

```javascript
const person = {
  firstName = "poco",
  lastName = "jang",
  // Concise Method
  getFullName() {
    return this.firstName + " " + this.lastName;
  },
};
```

<br/>
<br/>

## 정리)

모던 자바스크립트(ES2015+)부터

`shorthand properties`: Object에서 `key명 과 value명이 같`을 시 `하나의 명으로 축약` 가능<br/>

`Concise Method`: `key, value 구분 없(:)`이 함수(method) 선언 가능

<br/>

### 의문점)

익명합수(arrow func)도 값으로써 `Shorthand Properties`처럼 축약 가능하나, 외부에 선언된 변수를 참조하여 해당하는 객체의 변수를 가져오지 못함.

> 🤔 그럼 this가 참조하는 객체는 뭐지? -> 의문점 해결 안됨.

```javascript
const firstName = "poco";
const lastName = "jang";

const getFullName = () => {
  return this.firstName + " " + this.lastName;
};

const person = {
  firstName,
  lastName,
  getFullName,
};

person.firstName; // 'poco'
person.lastName; // 'jang'
person.getFullName(); // undefined undefined
```
