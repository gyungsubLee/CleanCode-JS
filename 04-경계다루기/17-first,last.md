# first, last

> 경계 다루기 (first, last)
> 1. 포함된 양 끝을 의미 (부터 ~~ 까지)

<br/><br/>

## ```최소(min)``` 와 ```최대(max)```의 특성

<img src="https://user-images.githubusercontent.com/95308384/195274563-55ffa605-e30d-4c11-baea-26f0bb41d803.png" width=60% />


```최소(min)``` 와 ```최대(max)```는 가장 작은 값과, 가장 큰 값을 의미한다. 즉, 비교 될 수 있는 범위인 ```수```를 나타낼 때 쓴다. 

또한 ```최소(min)``` 와 ```최대(max)```가 양 끝 경계에 위치하기 위해서는 최소(min), 최대(max) 포함된 집합은 ```연속(정렬)된 속성```을 가져야 한다.

이러한 2가지 특성을 만족할 때, ```최소(min)``` 와 ```최대(max)```는 명시적인 유효성을 갖는다.

<br/><br/>

## ```first``` 와 ```last```의 특성

그러나 ```first``` 와 ```last```의 경우, ```처음``` 과 ```마지막```, 즉 해당하는 요소들의 ```순서```만을 표현한다는 것에서 ```최소(min)``` 와 ```최대(max)``` 다르다.

즉, ```연속(정렬)되지 않는 집합```을 표현하는데 쓰인다. 

따라서 ```first``` 와 ```last```는 이름에 대한 집합, 정렬되지 않는 수에 대한 집합, html-dom 등 에 사용한다.

<br/>

### ex1) name 집합 (Array)
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
```min```, ```max```는 ```정렬된 수의 집합의 최소, 최대 값```을 나타낼 때 씀,

```first```, ```last는``` ```정렬되지 않는 집합의 처음과 마지막 순서```를 나타낼 때 씀.

