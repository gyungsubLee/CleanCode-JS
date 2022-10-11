# isNaN

```
1o 진수 -> 사람
---------------
    변환           간극 ->  소수점 주의
---------------
2 진수  -> 컴퓨터
```

이 간극을 javascript는 [IEEE 754](https://ko.wikipedia.org/wiki/IEEE_754) 표준을 사용하여 [부동소수점](https://ko.wikipedia.org/wiki/부동소수점) 방식으로 정의한다.
> 해당 표현이 맞는지 모르겠음...


<br/>
<br/>


## isNaN 
'is Not a NUmber'의 줄임 표현으로 NaN(Not-A-Number) 유무를 판별한다.

**느슨한 검사**를 하기 때문에 혼란스러은 케이스를 가지고 있으므로 ES2015+의 ```Number.isNaN()```을 사용하는 것이 좋다.

<br/>


## ```Number.isNaN()```
isNaN을 보완하기 위해 ECMAScript 2015부터 추가되었다. <br/>
```Number.isNaN()```을 사용하여 **엄격한 검사**를 할 수 있다.


<br/><br/>

## 정리

```Number.isNaN()``` 을 사용하여 안전하게 NaN 판별할 수 있다.

>isNaN: 느슨한 검사
>
>Number.isNaN:  엄격한 검사



<br/>

--- 
Reference)<br>
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/isNaN


겁나게 헷갈림... <br/>
다시 공부 후 이해후 testCase 정리하기