# ✍️ var 지양하기

### var 대신, let, const 사용

<br/>

var: 함수 스코프<br>

let, const: 블록 스코프, TDZ(Temporal Dead Zone) -> 안전하게 코드 작성<br>
> let, const: ES 2015 부터 추가

<br/><br/>

## var 사용 시 문제점

```javascript
var name = '이름';
var name = '이름2';
var name = '이름3';

console.log(name) // 이름3
```

```이미 선언한 변수를 다시 선언해도 error가 발생되지 않는다.```<br/>
 -> 이미 선언한 변수를 다시 선언해도 error를 반환하지 않으니 앱에 심각한 오류를 발생시킴.

### ```var```: 재선언(중복선언) 가능

<br>

```javascript
console.log(name) //undefined

var name = '이름3';
```

선언되기 전 변수를 가져와도 error가 나지 않고 undefined를 return 한다.

<br/><br/>

## let, const 사용을 통한 해결

### ```let```, ```const``` 사용 시 재선언(중복선언) 시 error를 발생시켜 ```var```의 문제점 해결됨.


<br>

### ```let```: 재선언 불가, 재할당 가능

```javascript
let name = '이름'
let name = '이름2' // 재선언 시 error 반환

name = '이름2' // 재할당 가능
```

<br/>

### ```const```: 재선언, 재할당 불가

```javascript
const name = '이름'
const name = '이름1' // error 반환 (재선언 불가)

name = '이름2' // error 반환 (재할당 불가)
```

<br/><br/>




