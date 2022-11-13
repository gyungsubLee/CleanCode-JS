# Optional Chainning(?.)

Optional Chainning(?.)는 참조하는 데이터가 `nullish(null or undefined)`이면 error를 대신하여 `undefined return` 한다. (함수도 가능)

따라서 `옵셔널 체이닝(optional chaining) ?.`을 사용하면 `프로퍼티가 없는 중첩 객체를 에러 없이 안전하게 접근`할 수 있다.

<br/>

```javascript
const adventurer = {
  name: "Alice",
  cat: {
    name: "Dinah",
  },
};

const dogName = adventurer.dog?.name;
console.log(dogName); // undefined

console.log(adventurer.someNonExistentMethod?.()); // undefined
```

<br/><br/>

## 옵셔널 체이닝이 필요한 이유

### Case1 - User address Object

`사용자의 주소 정보를 저장하는 중첩 객체`에 접근하는데, 몇몇 `사용자는 주소 정보가 없`다고 가정 시, 아래와 같이 error가 발생한다.

```javascript
let user = {}; // 주소 정보가 없는 사용자

alert(user.address.street); // TypeError: Cannot read property 'street' of undefined
```

<br/>

#### ● `and 단축평가(short-circuit) [&&]`

```javascript
let user = {}; // 주소 정보가 없는 사용자

alert(user && user.address && user.address.street); // undefined, 에러가 발생하지 않습니다.
```

옵셔널 체이닝 `전`에는 위 코드와 같이 `단축평가 and(&&)`를 사용하여 error를 대신하여 `undefind return` 처리를 하였다.

<br/>

#### ● `Optional Chainning(?.)`

```javascript
let user = {}; // 주소 정보가 없는 사용자

alert(user?.address?.street); // undefined, 에러가 발생하지 않습니다.
```

옵셔널 체이닝을 통해 간단하게 해결할 수 있다.

<br/>
<br/>

## `함수`에서의 Optional Chainning

```javascript
const result = someInterface.customMethod?.(); // omeInterface.customMethod는 정의 되지 않았음.

conosole.log(result); // undefined
```

`정의되지 않는 함수(null or undefined)` 또한 `Optional Chainnig(?.)`을 통해
안전하게 처리 가능하다.(return undefined)

<br/>
<br/>

## `단축 평가(short-circuit)`로써의 Optional Chainning

단축 평가는 [05-분기다루기/23 chapter](<../05-%EB%B6%84%EA%B8%B0%EB%8B%A4%EB%A3%A8%EA%B8%B0/23-%EB%8B%A8%EC%B6%95%ED%8F%89%EA%B0%80(%26%26%2C%7C%7C).md>)에서 따로 정리 했듯이 왼쪽에서 오른쪽으로 대상을 평가 진행하며, `값이 없을 시(nullish)` `즉시 평가를 멈`춘다.

따라서 `Optional Chainning(?.)` 이러한 단축 평가에 속하여 `평가 대상이 nullish(null, undefined)인 경우 평가를 멈`춘다.

```javascript
let user = null;
let x = 0;

user?.sayHi(x++); // 아무 일도 일어나지 않습니다.

alert(x); // 0, x는 증가하지 않습니다.
```

<br/>
<br/>

## `?.()`와 `?.[]`

`?.`은 연산자가 아닌 `함수나 대괄호와 함께 동작`하는 특별한 문법 구조체(syntax construct)이다.

`존재 여부가 확실치 않`는 `method`나 `property`에 접근 시 `?.()` 나 `?.[]`를 어떻게 사용하는지 예시를 알아보자.

<br/>

(`user 객체는 존재`하기 때문에 admin 프로퍼티는 `.`만 사용해 접근하였음.)

<br/>

### ● method - `?.()`

```javascript
let user1 = {
  admin() {
    alert("관리자 계정입니다.");
  },
};

let user2 = {};

user1.admin?.(); // 관리자 계정입니다.
user2.admin?.();
```

user1엔 admin이 정의되어 있기 때문에 메서드가 제대로 호출되었으나,` user2엔 admin이 정의되어 있지 않았음`에도 불구하고 `메서드를 호출`하면 `에러 없이 그냥 평가가 멈`추는 것을 확인 할 수 있다.

<br/>

### ● property - `?.[]`

```javascript
let user1 = {
  firstName: "Violet",
};

let user2 = null; // user2는 권한이 없는 사용자라고 가정해봅시다.

let key = "firstName";

alert(user1?.[key]); // Violet
alert(user2?.[key]); // undefined

alert(user1?.[key]?.something?.not?.existing); // undefined
```

위와 동일하게 `정의되지 않는 property`도 error 없이 `undefined return`

<br/>

### ● `?.` + `delete`

```javascript
delete user?.name; // user가 존재하면 user.name을 삭제합니다.
```

위와 같이 user 존재 시, delete method 정상 실행된다.

<br/>
<br/>

## Optional Chainning(?.) value 할당 불가능

```javascript
user?.name = "Violet"; // SyntaxError: Invalid left-hand side in assignment
// 에러가 발생하는 이유는 undefined = "Violet"이 되기 때문입니다.
```

위 예시와 같이` Optional Chainnig(?.)`을 통한 `쓰기`는 불가능하다.

<br/>
<br/>

## 정리)

1. `obj?.prop` – `obj가 존재`하면 `obj.prop을 반환`하고, 그렇지 `않`으면 `undefined를 반환`함
2. `obj?.[prop]` – `obj가 존재`하면 `obj[prop]을 반환`하고, 그렇지 `않`으면 `undefined를 반환`함
3. `obj?.method()` – `obj가 존재`하면 `obj.method()를 호출`하고, 그렇지 `않`으면 `undefined를 반환`함

. 왼쪽 평가 대상이 null이나 undefined인지 확인하고 null이나 undefined가 아니라면 평가를 계속 진행(short-circuit)

`?.`를 계속 연결해서 체인을 만들면 `중첩 프로퍼티들에 안전하게 접근`할 수 있음.

`?.`은 `?.왼쪽 평가대상이 없어도 괜찮은 경우`에만 선택적으로 사용해야함. `꼭 있어야 하는 값인데 없는 경우`에 `?.을 사용`하면 `프로그래밍 에러를 쉽게 찾을 수 없`다.

<br/>
<br/>

---

Reference)<br/>
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining<br/>
https://ko.javascript.info/optional-chaining<br/>
