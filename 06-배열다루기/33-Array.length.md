# Array.length 주의점

## 주제1 - `Array.length`는 배열의 길이가 아닌 `배열의 마지막 요소의 (index+1)`이다.

JavaScript에서의 `Array.length`는 배열의 길이가 아닌 `배열의 마지막 index`에 가깝다.

```javascript
const arr = [1, 2, 3];

console.log(arr.length); // 3

arr.length = 10;

console.log(arr.length); // 10

arr; // [1, 2, 3, , , , , , , ]
```

<br/>

```javascript
const arr = [1, 2, 3];

arr[3] = 4;

console.log(arr.length); // 4
console.log(arr); // [1, 2, 3, 4]

arr[9] = 10;

console.log(arr.length);
console.log(arr); // [1, 2, 3, 4, , , , , , 10]
```

<br/>
<br/>

## 주제2 - `Array.length` 역이용

### `Array.length = 0` -> 배열 초기화

```javascript
Array.prototype.clear = function () {
  this.length = 0;
};

function clearArray(array) {
  array.length = 0;

  return array;
}
```

<br/>

```javascript
const arr = [1, 2, 3];

arr.clear(); // []
clearArray(arr); // []
```

<br/>
<br/>

## 정리)

JavaScript에서의 `Array.length`는 배열의 길이가 아닌 배열의 `마지막 요소`의 index에서 1 더한 값(`idex + 1`)이다.

따라서 굉장히 헷갈릴 수 있기 때문에 의식적으로 헷갈리지 않게 사용 해야한다.

`arr.length = 0` 을 통해 배열 초기화 가능하다.
