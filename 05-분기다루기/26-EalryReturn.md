# Ealry Return

### 예시1 - 로그인 처리 함수

```javascript
function loginService(isLogin, user) {
  // 1. 로그인 여부 확인
  if (!isLogin) {
    // 2. 토큰 존재 여부 확인
    if (checkToken()) {
      // 3. 기가입 유저 확인
      if (!user.nickName) {
        // 가입X -> 가입
        return registerUser(user);
        // 가입 -> 로그인 처리
      } else {
        refreshToken();

        return "로그인 성공";
      }
    } else {
      throw new Error("No Token");
    }
  }
}
```

아래와 같이 `Ealry Return`을 통해 인간이 사고하기 편한 코드로 수정 가능함.
(로직은 변하지 않음.)

<br/>

```javascript
// Early Return
// 함수 미리 종료 -> 사고하기 편함

function loginService(isLogin, user) {
  // 1. 로그인 여부 확인
  if (isLogin) {
    return;
  }

  // 2. 토큰 존재 여부 확인
  if (!checkToken()) {
    throw new Error("No Token");
  }

  // 3. 기가입 유저 확인
  if (!user.nickName) {
    return registerUser(user);
  }

  refreshToken();

  return "로그인 성공";
}
```

`Ealry Return`을 사용하여 사람이 이해하기 쉽게 명시적으로 작성

<br/>
<br/>

### 예시2 -

```javascript
function 오늘하루(condition, weather, isJob) {
  if (condition === "GOOD") {
    공부();
    게임();
    유튜브보기();

    if (weather === "GOOD") {
      운동();
      빨래();
    }

    if (isJob === "GOOD") {
      야간업무();
      조기취침();
    }
  }
}
```

위 코드와 같이 로직이 하나의 조건에만 의존적으로 작성 되어 있을 때(하나의 의존성이 많은 로직을 묶여있는 경우), 아래와 같이 `Ealry Return'으로 코드를 분리하면 로직의 흐름을 간단하고 명시적으로 나태낼 수 있다.

<br/>

```javascript
function 오늘하루(condition, weather, isJob) {
  if (condition !== "GOOD") {
    return;
  }

  공부();
  게임();
  유튜브보기();

  if (weather === "GOOD") {
    운동();
    빨래();
  }

  if (isJob === "GOOD") {
    야간업무();
    조기취침();
  }
}
```

<br/>
<br/>

## 정리

`Ealry return`을 사용하여 사람이 이해하기 쉽게 명시적으로 코드 작성

`Ealry return`으로 의존성 분리 -> 명시적
