# min, max

> ### 경계 다루기 (min, max)
>
> 1.  최소, 최대 값 미리 변수로 만들어 놓기
>     (`MIN_`, `MAX_`)
>
> 2.  최소, 최대 값 포함 여부 `convention 정`하기
>
> 3.  변수명에 최솟값과 최대값 포함 여부를 표현하기 (`LIMIT`, `IN` 등)

<br>

## 1. 최솟값(min), 최댓값(max) 변수로 명시적 표현하기

```javascript
// 난수 생성 함수
function genRandomNumber(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

// 상수
const MIN_NUMBER = 1;
const MAX_NUMBER = 45;

genRandomNumber(MIN_NUMBER, MAX_NUMBER);
```

`최솟값(MIN_)`, `최댓값(MAX_)`을 위와 같이 `명시적으로 미리 선언`해 놓는다.

또한 위와 같이 `변수명을 명시적으로 작성`하면 `함수의 구현부를 보지 않아도 해당 함수의 의미를 이해`할 수 있다.

<br/><br/>

## 2. 경계를 포함 여부 (`이상`, `이하`),(`초과`, `미만`) convention 정하기

```javascript
const MIN_AGE = 20;

const isAdult = (age) => {
    if (age >= 20 or > 19){
        // ...some code
    }
}
```

위 예시인 성인 나이 유무를 판별하는 데 있어 `경계(최솟값)를 포함 유무`에 따라 `구분 짓는 데이터가 달`라진다.

또한 코드 복잡성이 증가할수록, 이러한 혼란성은 더욱 증가할 것이다.

따라서 `경계를 포함하는지, 포함하지 않는지` 모호하지 않게 `명시적으로 팀끼리 convention(기준)을 정`하여 써야한다.

<br><br>

## 3. 변수명을 통한 포함 여부 표현

```javascript
// LUMIT -> 초과, 미만
const MIN_NUMBER_LIMIT = 1;
const MAX_NUMBER_LIMIT = 45;

// IN -> 이상, 이하
const MIN_IN_NUMBER = 1;
const MAX_IN_NUMBER = 45;
```

위와 같이 `변수명` 통하여 `포함 여부`를 명시적으로 나타낼 수 있다.

<br/>
<br/>

## 정리

1. 최솟값 과 최댓값을 다룬다.

2. 최솟값, 최댓값 포함 여부(이상-초과 / 이하-미만) 팀원들끼리 convention을 정하여 사용한다.

3. 변수명에 최솟값과 최대값 포함 여부를 표현한다.
