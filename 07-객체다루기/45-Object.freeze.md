# 45. Object.freeze

`Object.freeze`는 의미 그대로 `객체를 동결`시킨다. typescript에서의 readonly와 유사하다.

```javascript
const STATUS = Object.freeze({
  PENDING: "PENDING",
  SUCCESS: "SUCCESS",
  FAIL: "FAIL",
});

Object.isFrozen(STATUS.PENDING); // true
Object.isFrozen(STATUS.SUCCESS); // true
Object.isFrozen(STATUS.FAIL); // true
```

`Object.isFrozen`을 통해 객체의 동결성 유무를 확인할 수 있다.

<br/><br/>

## `Object.freeze`의 문제점

`Object.freeze`은 `'깊은 복사(deep copy)'`가 일어나는 영역은 `관여하지 못`한다. 즉, `중첩 구조의 데이터`는 `동결되지 않`는다.

```javascript
const STATUS = Object.freeze({
  PENDING: "PENDING",
  SUCCESS: "SUCCESS",
  FAIL: "FAIL",
  OPTIONS: {
    GREEN: "GREEN",
    RED: "RED",
  },
});

Object.isFrozen(STATUS.OPTIONS); // false

// Update
STATUS.OPTIONS.GREEN = "G";

// Create
STATUS.OPTIONS.YELLOW = "Y";

console.log(STATUS.OPTIONS); // { GREEN: 'G', RED: 'RED', YELLOW: 'Y' }

// Delete
delete STATUS.OPTIONS.RED;

console.log(STATUS.OPTIONS); // { GREEN: 'G', YELLOW: 'Y' }
```

따라서 위 예시와 같이 `중첩된 객체 데이터인 OPTIONS`는 `CRUD` 시 `동결되지 않`고 정상적으로 `동작`된다.

<br/><br/>

## 중첩된 데이터 freezing 처리하기

> 1.  대중적인 유틸 라이브러리 >>(lodash)
> 2.  직접 유틸 함수 생성
> 3.  stackoverflow
> 4.  TypeScript => readonly

<br/>

### 2. 직접 유틸 함수 생성

```javascript
const STATUS = Object.freeze({
  PENDING: "PENDING",
  SUCCESS: "SUCCESS",
  FAIL: "FAIL",
  OPTIONS: {
    GREEN: "GREEN",
    RED: "RED",
  },
});

// 직접 유틸 함수 작성
const deepFreeze = (targetObj) => {
  // 1. 객체 순회
  // 2. 값이 객체인지 확인
  // 3. 객체 시 재귀
  // 4. 그렇지 않으면 Object.freeze

  Object.keys(targetObj).forEach(key => {
    if (/** 객체가 맞다면 */){
        deepFreeze(targetObj[key])
    }
  })

  return Object.freeze(targetObj);
};
```

위와 같이 `Object 유무 확인` 후 `재귀`를 통해 내부 데이터 구조에 접근하여 `Object.freeze` 처리를 하는 직접 유틸 함수(deepFreeze) 작성하여 처리 가능하다.

따라서 `깊은 영역까지 동결`시키기 위해 `팀`에서 `해당 유틸 함수를 정`하여 `안전하게 코드 작성`을 해야한다.

<br/>

### 4. TypeScript -> readonly

TypeScript 사용 시, readonly를 사용하여 읽기만 가능한 freeze 처리를 할 수 있다.

<br/>
<br/>

## 정리)

`Object.freeze` 데이터를 동결시켜 수정이 불가한 형태로 만든다.

그러나` 깊은 영역은 관여할 수 없`어
`중첩된 구조를 가진 데이터는 동결되지 않`는다.

<br/>

따라서 팀에서 `직접유틸함수`를 만들어 안전하게 내부 데이터까지 동결 처리하자.

> 직접유틸함수(deepFreeze)<br/>
> 객체 순회 -> 객체 유무 확인-> 객체 시 재귀 호출 -> 객체 아닐 시 Object.freeze 처리

<br/>

또한 `TypeScript`를 사용하여 `readonly` 처리를 하여도 가능하다.
