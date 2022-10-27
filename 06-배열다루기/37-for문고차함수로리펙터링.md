# for문 고차함수로 리펙터링

`고차함수`로 리펙토링하여 `명시적`으로 코드 작성하기

## case1 - 원화 표기

```javascript
// 1. 원화 표기

const price = ["2000", "1000", "3000", "5000", "4000"];

function getWonPrice(priceList) {
  let temp = [];

  for (let i = 0; i < priceList.length; i++) {
    temp.push(priceList[i] + "원");
  }

  return temp;
}

const result = getWonPrice(price);

console.log(result); // ["2000원", "1000원", "3000원", "5000원", "4000원"]
```

<br/>

### 리펙토링 [ for문 -> `map()` ]

```javascript
const price = ["2000", "1000", "3000", "5000", "4000"];

function getWonPrice(priceList) {
  return priceList.map((price) => price + "원");
}

const result = getWonPrice(price);

console.log(result); // ["2000원", "1000원", "3000원", "5000원", "4000원"]
```

<br/>
<br/>

## case2 - 1000원 초과 리스트만 출력

```javascript
// 1. 원화 표기
// 2. 1000원 초과 리스트만 출력

const price = ["2000", "1000", "3000", "5000", "4000"];

function getWonPrice(priceList) {
  let temp = [];

  for (let i = 0; i < priceList.length; i++) {
    if (priceList[i] > 1000) {
      temp.push(priceList[i] + "원");
    }
  }

  return temp;
}
```

<br/>

### 리펙토링 [ if문 -> `filter()` ]

```javascript
const price = ["2000", "1000", "3000", "5000", "4000"];

// 함수 내부 로직 -> 변수
const suffixWon = (price) => price + "원";
const isOverOneThousand => (price) => Number(price) > 1000;

function getWonPrice(priceList) {
  const isOverList = priceList.filter(isOverOneThousamd);

  return isOverList.map(suffixWon);
}
```

<br/>
<br/>

## Case3 - 가격순 정렬

```javascript
// 1. 원화 표기
// 2. 1000원 초과 리스트만 출력
// 3. 가격 순 정렬

const price = ["2000", "1000", "3000", "5000", "4000"];

// 함수 내부 로직 -> 변수
const suffixWon = (price) => price + "원";
const isOverOneThousand => (price) => Number(price) > 1000;

function getWonPrice(priceList) {
  const isOverList = priceList.filter(isOverOneThousamd);

  return isOverList.map(suffixWon);
}
```

또다른 조건 추가 시 filter를 통한 조건 추가? -> -다음 쳅터 '[메서드 체이닝](./38-메서드체이닝.md)'에서 해결

<br/>
<br/>

## 정리

고차함수로 코드를 명시적으로 작성

for문 -> `map()`<br/>
if문 -> `filter()`
