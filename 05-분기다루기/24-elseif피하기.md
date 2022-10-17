# else if 피하기

`else if`를 `promise의 than-chaining`하고는 같지 않다.(착각하는 경우가 있다고 함.)

![image](https://user-images.githubusercontent.com/95308384/196172193-90048b2f-1dfc-4169-9c9c-e397b5f627bf.png)

<br/>

`else if`는` else -> if`의 축약형이다.

### 예시1) else if

```javascript
const x = 1;

if (x >= 0) {
  console.log("x는 0과 같거나 크다"); // -> 실행
} else if (x > 0) {
  console.log("x는 0보다 크다"); // -> 실행X
}
```

<br/>

### `else if`는 `else -> if` 와 같다.

```javascript
if (x >= 0) {
  console.log("x는 0과 같거나 크다");
} else {
  if (x > 0) {
    console.log("x는 0보다 크다");
  }
}
```

`else if`는 위와 같이 `if/else 평가` 후 `if문 평가` 된다.

따라서 `else if`는 사용하지 않는 것이 좋다.
`if/else(조건)가 많`은 경우 -> `switch문`을 사용하는 것 권장

<br/>
<br/>

## 정리

`else if`는 `else -> if` 처리 이다. 따라서 사용하지 않는 것을 권장한다.

`if/else(조건)가 많`을 경우 -> `switch문`으로 대처한다.
