# undefined, null

<img src="https://user-images.githubusercontent.com/95308384/195045756-249ab0dd-1781-4570-a508-dfb4bd877dd6.png" width=60%> 


<br/>


### null: '없다'를 명시적으로 표현 한 것

### undefined: 무언가를 만들고 정의하지 않은 것, 초기화 상태

```javascript
let varb;

typeof varb   // 'undefined'
```




<br/><br/>

## null 과 undefined 형 변환

```javascript
!undefined  //true
!null       // true
!!null      // false

null === false   // false
!null === true   // true
```


```javascript
undefined == null      // true
undefined === null     // false
!undefined === !null   // true
```

자세한 내용은 [13-형 변환 줄이기](./13-형변환줄이기) 참조


<br/><br/>

##  null 과 undefined 숫자형 변환

### null -> 0, undefined -> NaN

```javascript
// null =>  0
null + 123    ->  123
```

```javascript
// undefined => Not a Number
undefined + 10   -> NaN
```

<br/><br/>



## 정리
<img src="https://user-images.githubusercontent.com/95308384/195052344-226f922c-8575-4e50-9a3f-cf522f5233a4.png" width=60%> 

<br/>

```null```: '없다'를 명시적으로 표현<br>
```undefined```: 무언가를 만들고 정의하지 않은 것

<br/>

undefined 나 null 로 작성하는 코드 줄이기(```↓```)

<br/>

팀으로 작업 시 ```비어있는 값(null, undefined)```을 무엇을 사용할 것인지 ```convention을 정```하는 것이 좋음


<br/>

----

Reference)<br/>
https://antstudy.tistory.com/48
ㅍ