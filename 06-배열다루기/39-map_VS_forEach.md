# map 과 forEach 차이점

자바스크립트의 배열 메서드를 사용하면서 첫번쨰로 많이 하는 실수가 `map` 과 `forEach`의 정확한 사용법을 몰라 `map` or `forEach` 만 사용하는 것이다.

따라서 해당 문서에서 `map` 과 `forEach`의 각각의 쓰임세를 정리하면서 적절한 상황에 사용하자.
<br/>
<br/>

## 차이점 - `return 유무`

```javascript
const prices = ['1000', '2000', '3000' ];

// forEach
const newPricesForEach = prices.forEach(price => return price + '원');

console.log(newPricesForEach); // undefined

// map
const newPricesMap = prices.map(price => return price + '원');

console.log(newPricesMap); // ['1000', '2000', '3000' ]
```

forEach -> `undefined` return

map -> `new Array` return

<br/>

#### ● [MDN - forEach](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

forEach는 주어진 요소를 하나 씩 돌리면서 `콜백으로 들어오는 매개변수 함수를 실행`시킨다. 그리고 `undefined를 반환`한다.

<br/>

#### ● [MDN - map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

map은 주어진 배열의 `각 요소`를 돌면서 `콜백 매개변수 함수의 결과 값`으로 된 `새 배열을 반환`한다.

<br/>
<br/>

## 정리)

언어의 명세에서

`map`은 `새로운 배열`을 만들 때 사용,

`forEach`는 `요소가 루프를 돌`면서 `특정 함수를 실행`시킬 때 사용

한다라고 명시되어 있다.

따라서 해당 쓰임에 맞게 적절하게 사용하자.
