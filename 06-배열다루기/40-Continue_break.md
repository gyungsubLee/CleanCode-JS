# Continue & Break

## 배열 메서드 사용 시 자주하는 실수2 - continue, break

`배열 메서드(map, forEach ...)` 사용 시, for문에서 처럼 `루프를 중단`하기 위해 아래와 같이 `continue` 나 `break`을 사용하는 경우, `오류(SyntaxError)`가 발생한다.

<br/>

```javascript
const orders = ['first', 'second', 'third'];

orders.forEach(function(order) {
    if(order === 'second') {
        continue; // SyntaxError
        break; // SyntaxError
    }

    console.log(order);
})
```

<br/><br/>

## try - catch 를 통한 해결

```javascript
const orders = ['first', 'second', 'third'];

// try - catch
try {
    orders.forEach((order) => {
        if(order === 'second') {
            throw
        }
    });
} catch(e) {
  // ...some code
}
```

<br/><br/>

## for문 / for-of문 / for-in문

해결 방법 중 하나로써 다시 for문을 사용하는 것이다.

for문에서는 continue 와 breack 정상적으로 동작하기 때문에 의도한대로 흐름을 제어 할 수 있다.

<br/>

```javascript
const orders = ["first", "second", "third"];

// for문
for (let index = 0; index < array.length; index++) {
  const element = array[index];
  // ...some code
}

// for-of문
for (const iterator of object) {
  // ...some code
}

// for-in문
for (const key in object) {
  // ...some code
}
```

<br/><br/>

## 배열 메서드(`every()`, `some()`, `find()`, `findIndex()`)

해당하는 `배열메서드(every(), some(), find(), findIndex())`는 요소를 판별하여 true/false 여부에 따라 반`복(루프)의 종료 여부를 결정`한다.

<br/>
<br/>

## 정리)

<img src="https://user-images.githubusercontent.com/95308384/198580947-ca8a5714-1d3d-4a6b-8096-fac8d5ba0441.png" width=60% />

-[MDN\_\_forEach 참조](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

<br/>

forEach, map 등 continue, break으로 루프 제어 불가능

### 해결방법

1. try-catch
2. for문/for-of문/for-in문
3. 배열 메서드 - every(), some(), find(), findIndex()

<br/>

> try - catch, 배열메서드(every(), some(), find(), findIndex()) 추가 정리
