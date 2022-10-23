# JavaScript의 배열은 객체다.

## 주제1 - Array == Object

### ● Array

```javascript
const arr = [1, 2, 3];

arr[3] = "test";
arr["property"] = "string value";
arr["obj"] = {};
arr[{}] = [1, 2, 3];
arr["func"] = function () {
  return "hello";
};
```

배열 선언 후, 요소를 object 형태(key:value)로 추가 시, 해당 배열에 정상적으로 추가된다.

<br/>

```javascript
console.log(arr);
// [1, 2, 3, 'test', property: 'string value', obj: {}, '[object Object](형변환-문자열)': [1, 2, 3], func: [λ(함수)]]
```

해당 배열 출력 시, 모든 property가 추가되어 출력되는 것을 볼 수 있다.

<br/>

```javascript
//while문 -> for문 축소
let i = 0;
whlie(i < arr.length) {
    i++;
} => x arr.length


for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}
// 1 2 3 test
```

다른 property들이 출력되지 않는 것은 key(`[i]`)를 숫자로만 설정해서 그렇다.

<br/>

### ● Object

```javascript
const obj = {
  arr: [1, 2, 3],
  3: "test",
  property: "string value",
  obj: {},
  "{}": [1, 2, 3],
  func: function () {
    return "hello";
  },
};

console.log(obj);

// [1, 2, 3], 'test', property: 'string value', obj: {}, '[object Object]': [1, 2, 3], func: [λ]
```

object로 만들어도 동일하다.

<br/>

```javascript
const arr = [1, 2, 3];

const obj = {
0: 1,
1: 2, 2, 2: 3}
```

따라서 Array는 `index를 key로 갖는 object`와 같다고 볼 수 있다.

<br/><br/>

## 주제2 - 배열 판단 (Array.isArray())

```javascript
const arr = [1, 2, 3];
const arr2 = `[1, 2, 3]`;

Array.isArray(arr); // true
Array.isArray(arr2); // false
```

<br/>

```javascript
const arr = [1, 2, 3, 'test', property: 'string value', obj: {…}, [object Object]: Array(3), func: ƒ]

Array.isArray(arr); // true
```

위 경우도 Array로 판단한다.

<br/><br/>

## 정리)

JavaScript에서` Array(배열)`은 `Object(객체)`임

배열 판단 -> `Array.isArray()` 사용
