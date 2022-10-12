# first, last

> 경계 다루기 (first, last)
> 1. 포함된 양 끝을 의미 (부터 ~~ 까지)

<br/>

<img src="https://user-images.githubusercontent.com/95308384/195274563-55ffa605-e30d-4c11-baea-26f0bb41d803.png" width=60% />


```min``` 과 ```max```의 경우, 위 그림과 같이 ```두 경계 사이의 범위에 연속성이 존재```하여, 순차적으로 모든 요소에 대해 처리할 때, 명시적인 유효성이 있다.

<br/>

그러나 ```first``` 와 ```last```의 경우 min/max와 같이 ```처음``` 과 ```마지막```을 나타낸 다는 점이 비슷하면서도 ```연속성이 존재하지 않는다(규칙이 없다)```는 점이 다르다.

<br/>

### ex1) Array 요소
```javascript
const students = ['LEE', 'KIM', 'HAN'];

function getStudents(first, last){
    // ...some code
}

getStudents('LEE', 'HAN');
```
<br/>

### ex2) html-dom
```javascript
element.firstChild
element.lastChild
```


<br>
<br>

## 정리
### first, last
```first```부터 ```last```까지의 범위<br/>
연속성(규칙) X