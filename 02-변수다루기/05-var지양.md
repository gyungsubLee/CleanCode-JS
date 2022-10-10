# ✍️ var 지양하기

### var: 함수 스코프<br>

### let, const: 블록 스코프, TDZ(Temporal Dead Zone) -> 안전하게 코드 작성<br>

<br>

>### 🤚 함수 레벨 스코프(Function-level scope) - ```var```
>함수 내에서 선언된 변수는 함수 내에서만 유효하며 함수 외부에서는 참조할 수 없다.<br/> 즉, 함수 내부에서 선언한 변수는 지역 변수이며 함수 외부에서 선언한 변수는 모두 전역 변수이다.
>
>### 🤚 블록 레벨 스코프(Block-level scope) - ```let```, ```const```
>모든 코드 블록(함수, if 문, for 문, while 문, try/catch 문 등) 내에서 선언된 변수는 코드 블록 내에서만 유효하며 코드 블록 외부에서는 참조할 수 없다.<br/> 즉, 코드 블록 내부에서 선언한 변수는 지역 변수이다.

<br/><br/>

# var 사용 시 문제점

## 1. 함수 레벨 스코프(Function-level scope)

함수의 코드 블록만을 스코프로 인정한다. 따라서 전역 함수 외부에서 생성한 변수는 모두 전역 변수이다. 이는 전역 변수를 남발할 가능성을 높인다.<br/>

블록 레벨 스코프 (for문, if문 등)의 변수 선언문에서 선언한 변수를 for 문의 코드 블록 외부에서 참조할 수 있다.

=> 자세한 내용 [06-함수/블록 스코프.md](./06-%ED%95%A8%EC%88%98_%EB%B8%94%EB%A1%9D-%EC%8A%A4%EC%BD%94%ED%94%84.md) 참조

<br/>

## 2. var 키워드 생략 허용
암묵적 전역 변수를 양산할 가능성이 크다.
 
<br/>

## 3. 변수 중복 선언 허용
변수의 중복 선언을 하여 ```의도하지 않은 변수값의 변경```이 일어날 가능성이 크다.

```javascript
var name = '이름';
var name = '이름2';
var name = '이름3';

console.log(name) // 이름3
```

```이미 선언한 변수를 다시 선언해도 error가 발생되지 않는다.```<br/>
 -> 이미 선언한 변수를 다시 선언해도 error를 반환하지 않으니 앱에 심각한 오류를 발생시킴.


<br>

## 4. 변수 호이스팅
변수를 선언하기 이전에 참조함.

```javascript
console.log(name) //undefined

var name = '이름3';
```

선언되기 전 변수를 가져와도 error가 나지 않고 undefined를 return 한다.

<br/>

대부분의 문제는 전역변수로 인해 발생한다.
전역 변수는 유효 범위(scope)가 넓어서 어디에서 어떻게 사용될 것인지 파악이 힘들며, 비순수 함수(Impure function)에 의해 의도치 않게 변형될 수 있어 복작성을 증가시키는 원인이 된다. 

따라서 변수의 스코프는 좁을 수록 좋으며, 이러한 var 단점을 보완하기 위해 ES6부터 ```let``` 과 ```const``` 키워드가 도입되었다.


<br/><br/>

# let, const 사용을 통한 해결


## 3. 변수 중복 선언
### ```let```, ```const``` 사용 시 재선언(중복선언) 시 error를 발생시켜 ```var```의 문제점 해결됨.


<br>

### ```let```: 재선언 불가, 재할당 가능

```javascript
let name = '이름'
let name = '이름2' // Error (재선언 불가)

name = '이름2' // 재할당 가능
```

<br/>

### ```const```: 재선언, 재할당 불가

```javascript
const name = '이름'
const name = '이름1' // Error (재선언 불가)

name = '이름2' // Error (재할당 불가)
```

<br/>

## 4. 변수 호이스팅
호이스팅(Hoisting)이란, 선언문(var, function ...)을 해당 스코프 선두로 옮긴 것처럼 동작하는 특성을 말하며,
자바스크립트는 모든 선언(var, let, const, function, class)을 호이스팅한다.

var와 달리 ```let```, ```const```로 선언된 변수를 선언문 이전에 참조하면 ```참조 에러(ReferenceError)```가 발생한다. 이는 ```let```, ```const```로 선언된 변수는 스코프의 시작에서 변수의 선언까지 일시적 사각지대(Temporal Dead Zone, TDZ)에 빠지기 때문이다.

```javascript
console.log(foo); // undefined
var foo;

console.log(bar); // Error: Uncaught ReferenceError: bar is not defined
let bar;
```

<br/>

> ### 변수 생성 과정(3단계)
> #### 1. 선언 단계(Declaration phase)
>변수를 실행 컨텍스트의 변수 객체(Variable Object)에 등록한다. 이 변수 객체는 스코프가 참조하는 대상이 된다.
> #### 2. 초기화 단계(Initialization phase)
>변수 객체(Variable Object)에 등록된 변수를 위한 공간을 메모리에 확보한다. 이 단계에서 변수는 undefined로 초기화된다.
> #### 3. 할당 단계(Assignment phase)
>undefined로 초기화된 변수에 실제 값을 할당한다.


<br/>

## var
### ```var``` 키워드로 선언된 변수는 ```선언 단계와 초기화 단계가 한번```에 이루어 진다.
따라서, 스코프에 변수를 등록(선언 단계)하고 메모리에 변수를 위한 공간 확보 후, undefined로 초기화(초기화 단계)한다. 

따라서 변수 선언문 이전에 변수에 접근하여도 스코프에 변수가 존재하기 때문에 에러가 발생하지 않는다. (```undefined 반환```)<br/>이후 변수 할당문에 도달해 값이 할당(할당 단계)된다.

<br/>

## TDZ(let, const)
### 반면 ```let```, ```const```로 선언된 변수는 ```선언 단계와 초기화 단계가 분리```되어 진행된다.
즉, 스코프에 변수를 등록(선언단계)하지만 초기화는 변수 선언문에 도달했을 때 이루어진다.<br/>
초기화 이전에 변수에 접근하려고 하면 참조 에러(ReferenceError)가 발생하며 이는 변수가 아직 초기화되지 않았기 때문이다. 즉, 변수를 위한 메모리 공간이 아직 확보되지 않았기 때문이다. 따라서 스코프의 시작 지점부터 초기화 시작 지점까지는 변수를 참조할 수 없다. 그리고 스코프의 시작 지점부터 초기화 시작 지점까지의 구간을 ‘일시적 사각지대(Temporal Dead Zone; TDZ)’라고 부른다.



<br/>



<img src="https://user-images.githubusercontent.com/95308384/194788410-5c0d38d5-dc63-4ab8-82e0-47636c1ce73c.png" width=50%>

<br/>

```javascript
// 스코프의 선두에서 선언 단계가 실행 (Hoisting)
// 아직 변수가 초기화되지 않음. -> 참조 X

console.log(foo); // ReferenceError: foo is not defined

let foo; // 변수 선언문에서 초기화(메모리 공간 확보와 undefined로 초기화))
console.log(foo); // undefined

foo = 1; // 할당문에서 할당
console.log(foo); // 1
```

<br/>

```javascript
let foo = 1; // 전역 변수

{
  console.log(foo); // ReferenceError: foo is not defined
  let foo = 2; // 지역 변수
}
```

 ```let```으로 선언된 변수는 ```블록 레벨 스코프```를 가지므로 코드 블록 내에서 선언된 변수 foo는 지역 변수이다. 따라서 해당 스코프에서 호이스팅되고 코드 블록의 선두부터 초기화가 이루어지는 지점까지 TDZ에 빠진다. 따라서 전역 변수의 foo 값이 출력되지 않고 ReferenceError가 발생한다.


<br/>

## const
위에서 설명했듯이 ```const```는 재할당이 불가능하다. 따라서 ```선언과 동시에 할당이 이루어져야한다.```

그렇지 않을 시 아래와 같이 SyntaxError가 발생한다.

```javascript
// 스코프의 선두에서 선언 단계가 실행 (Hoisting)
// 아직 변수가 초기화되지 않음. -> 참조 X

console.log(foo); // ReferenceError: foo is not defined

const foo; // const는 선언과 할당이 동시에 이루어져야함.
console.log(foo); // SyntaxError: Missing initializer in const declaration

const foo = 1; 
console.log(foo); // 1
```

또한 블록 레벨 스코프를 가진다.

```javascript
{
  const FOO = 10;
  console.log(FOO); //10
}
console.log(FOO); // ReferenceError: FOO is not defined
```




----
Reference)<br>
https://poiemaweb.com/es6-block-scope



