# ProtoType 이해하기

> `__proto__` -> `[[Prototype]]` 변경

> ### ● keyword
>
> 1. Prototype vs Class -> 프로토타입기반 프로그래밍
> 2. Prototype - prototype object, prototype link

<br/>

JavaScript에서는 기본 데이터 타입인 boolean, number, string... 그리고 특별한 값인 null, undefined를 제외하고는 모두 객체(function, array ...)이다.

이러한 객체를 다루는데 있어 객체 지향 프로그래밍은 뺄 수 없는 패러다임일 것이다.

또한 객체 지향 프로그래밍을 다루는데 있어 클래스(Class)라는 개념은 거의 필수적이라고 볼 수 있다.

그러나 자바스크립는 객체지향언어이면서도 클래스라는 개념이 존재하지 않는다. 대신 프로토타입(Portorype)이 존재하며, 클래스를 대신하여 객체를 다룬다. 이러하여 자바스크립트가 프로토타입 기반 언어라고 불리우는 이유이다.

이러한 프로토타입을 이해하기 위해 이번 글을 정리한다.

<br/><br/>

## 프로토타입기반 프로그래밍

위에서 설명했듯이 JavaScript는 클래스(class)라는 개념이 없다,

따라서 보통 프로토타입을 기반으로 객체의 상속 및 확장을 흉내내도록 구현해 사용한다.

`객체 원형`인 `프로토타입`을 이용하여 `새로운 객체를 만`들어내며<br/>
또한 이렇게 생성된 객체 역시 `또 다른 객체의 원형`이 되며 `새로운 객체`를 만들어 낸다.([체이닝이 가능한 이유](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Object_prototypes#%ED%94%84%EB%A1%9C%ED%86%A0%ED%83%80%EC%9E%85_%EA%B8%B0%EB%B0%98_%EC%96%B8%EC%96%B4))

이리하여 자바스크립트는 프로토타입을 이용한 클로닝(Cloning: 복사)과 객체 특성을 확장해 나가는 방식으로 객체를 생성하여 객체 지향적인 프로그래밍 가능케한다.

<br/>

> ES6 표준에서 추가된 Class문법은 문법이 추가된 것이지 내부 로직은 prototype으로 동작한다.
>
> [강의 <class -> vabel 변환 이미지> 참조하기]

<br/>
<br/>

## 프로토타입의 응용

자바스크립에서는 클래스는 없지만 함수(function)와 new 키워드를 통해 클래스를 흉내낼 수 있다.

> 함수(function), new 키워드도 프로토타입이다.<br/> (new 연산자도 prototype 맞나?)

```javascript
function Person() {
  this.arms = 2;
  this.legs = 2;
}
var LEE = new Person();
var HAN = new Person();

console.log(LEE.arms); // => 2
console.log(LEE.legs); // => 2

console.log(HAN.arms); // => 2
console.log(HAN.legs); // => 2
```

LEE와 HAN은 'arm' 과 'leg' 속성을 공통적으로 가지고 있어, 메모리에서는 2개 씩 총 4개가 할당된다. 따라서 `객체의 개수가 증가`하면 그에 `비례`하여 `중복되는 변수`가 계속해서 `메모리에 할당`된다.

이러한 `연산 낭비`를 `프로토타입`을 통해 해결할 수 있다.

<br/>

```javascript
function Person() {} // Person 객체 생성
Person.prototype.arms = 2;
Person.prototype.legs = 1;
var LEE  = new Person();
var HAN = new Person():
console.log(LEE.arms);  //2
```

`Person() {}` 객체 생성 시, `Person.prototype이라는 Object가 생성`되고 , Person 함수로부터 생성된 객체(LEE, HAN)들은 Person.prototype를 원형으로 생성되어 `Person.prototype에 추가된 속성(arms, legs)들을 참조`하여 가져다 쓸 수 있다.

따라서 `객체가 늘`어나도 복사가 아닌 `참조`가 일어나 메모리에 변수들을 일일이 생성하지 않아 `메모리 공간을 낭비를 `줄인다.

<br/>

이러한 방식이 어떻게 동작하는지를 그 이유를 알기 위해 프로토타입에 대해 조금 더 깊에 알아보도록 하자.

<br/>
<br/>

## ● Prototype

Prototype의 단어 자체가 `원형`, `원본`이라는 의미를 말하는데 JavaScript에서 해당하는 뜻과 동일한 의미를 갖는다. 즉, `어떠한 객체가 만들어지기 위해 그 객체의 모태가 되는 객체`가 Prototype이다. 따라서 클래스(class)와 형태는 다르지만 유사한 의미를 지닌다.

Prototype은 `Prototype Link`, `Prototype Object`로 이루어져 있는데, 이 둘을 통틀어 Prototype이라 한다.

이러한 프로토타입을 이해하는데 있어 많은 도움을 받은 [[Javascript ] 프로토타입 이해하기- 오승환](https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67)님 포스트의 4가지 포인트를 인용하여 정리한다.

<br/><br/>

## Prototype Object

> ### ▶ Point 1 - 객체는 언제나함수(function)로 생성된다.

 <br/>

```javascript
function Person() {} // => 함수
const personObject = new Person(); // => 함수로 객체를 생성
```

personObject 객체는 Person이라는 함수로 생성된 객체이다. 이렇듯 언제나 객체는 함수에서 시작되며, 많이 쓰는 일반적인 객체 생성도 예외는 아니다.

```javascript
// 일반적인 객체 생성
var obj = {};

// 실제 해석되는 코드
var obj = new Object();
```

<br/>

그럼 이것이 Prototype Object와 무슨 상관이 있는지는 아래를 통해 설명한다.

일반적으로 함수가 정의될 때 2가지 일이 동시에 이루어진다.

<br/>

> ### ▶ point 2 - 해당 함수로 생성된 객체에 Constructor(생성자) 자격 부여

Constructor 자격이 부여되면 new 키워드를 통해 객체를 만들 수 있다. 이것이 함수만 new 키워드를 사용할 수 있는 이유이다.

<br/>

#### ● 일반 객체로 new 키워드 사용 시 상속 불가

![image](https://user-images.githubusercontent.com/95308384/200305152-b9172d8e-9935-495f-b6b4-e160f789a60f.png)

일반 객체로 생성된 객체는 constructor 자격이 부여되지 않는다. <br/>
따라서 new 키워드 사용시 위와 같은 오류가 발생한다.

<br/>

#### ● 함수로 생성한 객체 사용 시 가능

![image](https://user-images.githubusercontent.com/95308384/200304573-d85ff776-791b-4af3-8a87-e87dba781707.png)

함수로 생성된 객체에서는 contructor 자격이 부여돼 new 키워드로 인스턴스를 정상적으로 생성한다.

따라서 `함수를 통해서 생성된 객체`에 `constructor 자격이 부여`되며, 이를 통해서만 new 키워드를 통해 인스턴스를 생성할 수 있다.

<br/><br/>

> ### ▶ point 3 - 해당 함수의 Prototype Object 생성 및 연결

함수를 정의하면 함수만 생성되는 것이 아니라 Prototype Object도 같이 생성된다.

![esss](https://user-images.githubusercontent.com/95308384/200160824-d3692be9-2aed-4011-854d-6685fa97bcdd.png)

그리고 생성된 함수는 prototype이라는 속성 가지며 해당 속성을 통해 Prototype Object에 접근할 수 있다.

`Prototype Object`는 일반적인 객체와 같으며 기본적인 속성으로 `constructor`와 `[[Prototype]]`를 가지고 있다.

<br/>

![image](https://user-images.githubusercontent.com/95308384/200160709-b1c315fb-1778-447a-ac0f-6be3db4a927d.png)

위 그림과 같이 `Person.prototype`을 통해
`Prototype Object` 접근 가능한 것을 확인 할 수 있으며 `Prototype Object`는 같이 생성되었던 함수를 가리키는 constructor`와 `Prototype Link인 [[Prototype]](이전엔 **proto**)`을 속성으로 가진다.

<br/>

따라서 아래의 예시를 보면 왜 prototype을 사용하는지 이해할 수 있을 것이다.

```javascript
function Person() {}

Person.prototype.eyes = 2;
Person.prototype.nose = 1;

var kim  = new Person();
var park = new Person():

console.log(kim.eyes); // => 2
```

<br/>

![image](https://user-images.githubusercontent.com/95308384/200313824-f94ab951-b7e2-49e4-9114-e2e17ab009ed.png)

Prototype Object는 일반적인 객체이므로 property의 CRUD가 가능하다.

kim과 park은 Person 함수를 통해 생성되었으니 Person.prototype을 참조할 수 있다. (Prototype Link 통해 가능)

<br/>
<br/>

## Prototype link

![image](https://user-images.githubusercontent.com/95308384/200314758-2070a743-8646-453e-b08f-4f50552c069e.png)

kim에는 eyes라는 속성이 없는데도 kim.eyes를 실행하면 2라는 값을 참조하는 것을 볼 수 있다. 위에서 설명했듯이 Prototype Object에 존재하는 eyes 속성을 참조한 것인데, `Prototype Link`인 `[[Prototype]](__proto__)`을 통해 가능하다.

prototype 속성은 함수만 가지고 있던 것(Person.prototype)과는 달리

`Prototype Link([[Prototype]])`는 `모든 객체가 빠짐없이 가지`고 있는 속성이며 객체가 생성될 때 `조상이었던 함수의 Prototype Object`를 가리킨다.

kim객체는 Person함수로부터 생성되었으니 Person 함수의 Prototype Object를 가리키고 있는 것이다.

`kim.__proto__`를 출력해보면 아래와 같이 `조상 객체인 Person`을 가리키고 있는 것을 알 수 있다.

![image](https://user-images.githubusercontent.com/95308384/201077571-92639104-3c22-4c7c-9c7c-51ae0a909313.png)

![image](https://user-images.githubusercontent.com/95308384/200315408-c67c4dc0-a926-4b67-aeb0-32baab6954c4.png)

![image](https://user-images.githubusercontent.com/95308384/200315444-877d70fa-049d-4647-874f-d73ffac345f0.png)

이러한 `prototype link([[Prototype]])`를 통해 `체인 구조`가 형성되어 `체이닝`을 사용하여 `Object Prototype Object에 있는 모든 속성을 사용`할 수 있고 `모든 객체가 Object의 자식`임을 확인할 수 있다.

![image](https://user-images.githubusercontent.com/95308384/200315563-549017c9-7802-4ce8-911d-5e446998934f.png)

이러한 `prototype link([[Prototype]])`와 `프로토타입 체인`을 이해하는 것이 네 번째 포인트이다.

<br/>
<br/>

> 이해하는데는 그리 오래걸리지 않았지만 정리하는데는 참 오래걸렸다... <br/>
> 아직도 부족한 표현들이 많이 보이니 계속해서 수정해나가야 할 듯 하다...<br/>
> 1차 작성 - 11월 7일<br/>
> 2차 작성 - 11월 10일<br/>

<br/>

---

Reference)<br/>
https://www.nextree.co.kr/p7323/<br/>
https://medium.com/@bluesh55/javascript-prototype-이해하기-f8e67c286b67<br/>
http://insanehong.kr/post/javascript-prototype/<br/>
https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Object_prototypes#%ED%94%84%EB%A1%9C%ED%86%A0%ED%83%80%EC%9E%85_%EA%B8%B0%EB%B0%98_%EC%96%B8%EC%96%B4
