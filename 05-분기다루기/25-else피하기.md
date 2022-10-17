# else 피하기

```javascript
// user.name이 true/false 일떄
function getUserName(user) {
  if (user.name) {
    return user.name;
  } else {
    return "이름없음";
  }
}
```

위 예시는 user.name이 `true`일때, `false`일 때가 명백하게 나뉘어 짜여진 코드이다.<br/>
이와 같이 else문 사용 시, `논리적으로도 반대의 로직`이 함께 작성된다.

<br/>

## Error) else 사용, 1개 함수 -> 2가지 역활

하나의 함수는 1개의 역활만 하는 것이 이상적이다. 그러나 else문 사용 시 아래와 예시와 같이 하나의 함수가 2개의 역활을 할 수 있다.

<br/>

```javascript
/**
 * age가 20 미만시 특수 함수 실행
 */
function getHelloCustomer(user) {
  // else문 사용 예시
  if (user.age < 20) {
    report(user);
  } else {
    return "안녕하세요";
  }
```

성인이 아닌 경우에도 `return "안녕하세요";` 해당 로직이 실행되어야 하는데 else문을 사용때문에 실행되지 않는다.

<br/>

```javascript
// 게선 코드
function getHelloCustomer(user) {
  if (user.age < 20) {
    report(user);
  }
  return "안녕하세요";
}
```

위와 같이 else문을 제거, 정상 실행

<br/><br/>

## 정리)

항상 else를 쓸 필요는 없으며

위와 같은 오류가 발생하는 경우, else문을 제거하여 아래와 같이 작성한다.

```javascript
function getUserName(user) {
  if (user.name) {
    return user.name;
  }
  return "이름없음";
}
```

해당 내용은 후에 `early return `에서 다시 정리함. 따라서 추가 정리후 link 추가하기

<br/>

### -> 명확하게 이해가 안됨. 다시 학습 후 정리하기
