# 46. ProtoType 조작 지양하기

> [ProtoType](prototype.md) 정리

<br/>

Prototype 조작을 지양해야하는 이유는 초창기와 달리 이미 자바스크립트는 많은 발전을 해왔으며

자바스크립트는 [몽키 패치(Monkey patch)](https://en.wikipedia.org/wiki/Monkey_patch) 언어로써 런타임 시 동작되는 코드가 멋대로 변경될 수 있기 때문에

기본으로 제공하는 `빌트인 메소드들`을 사용하는 것이 더 `안전`하고 `명시적`이다.

<br/>

### 예전 코드 [ 클래스 -> 생성자 함수, prototype 조작 사용]

```javascript
function Car(name, brand) {
  this.name = name;
  this.brand = brand;
}

Car.prototype.sayName = function () {
  return this.brand + "-" + this.name;
};
```

<br/>

### 현재 코드 [클래스 문법 사용]

```javascript
class Car {
  constructor(name, brand) {
    this.name = name;
    this.brand = brand;
  }

  sayName() {
    return this.brand + "-" + this.name;
  }
}

const casper = new Car("캐스퍼", "현대");
```

<br/>
<br/>

## Case2 - prototype 조작

### prototype method 추가

![image](https://user-images.githubusercontent.com/95308384/201082146-c754b905-eab7-4c27-bf0a-cd7184ceb878.png)

위 예시를 보면 prototype을 조작하여 `welcome` method를 추가 및 실행 확인이 가능하다.

<br/>

### Array.forEach()

![image](https://user-images.githubusercontent.com/95308384/201083526-70d5dba0-d932-4c34-89a9-c60b6b732df3.png)

과거에는 빌트인 함수를 많이 renewal하여 사용하였다.

그러나 현재는 자바스크립트가 많이 발전하여 그럴 필요가 없다.

<br/>
<br/>

## Case3 - [marpple/Fx.js](https://github.com/marpple/FxJS)

![image](https://user-images.githubusercontent.com/95308384/201084221-3c646889-f524-4bd1-8ba2-db9ea19b11b6.png)

prototype을 조작하는 것이 아닌 `JavaScript 모듈`을 가져와서 조작한다.

<br/>
<br/>

## Case4 - [Lodash 라이브러리](https://lodash.com/docs/4.17.15#findIndex)

![image](https://user-images.githubusercontent.com/95308384/201085139-d96b9b11-0407-4780-85d8-815a2be90a9b.png)

이미 JavaScript에서 지원하는 method들이 존재하지만 Prototype을 조작하지 않는다.

<br/>
<br/>

## Case 4 - Class -> [Babel변환](https://babeljs.io/repl#?browsers=defaults%2C%20not%20ie%2011%2C%20not%20ie_mob%2011&build=&builtIns=false&corejs=3.21&spec=false&loose=false&code_lz=MYGwhgzhAEDCYCdoG8BQ1rAPYDsIBcEBXYfLBAChzAFsBTAGmgCMEwcATAShXQ2nwALAJYQAdNXrQAvNEl0A3HwxDRY1uw4yWbTkowBfVHwhgAngDladCjzT9oCOviIIcAkeI2doAamgARAC0AX4eavL60EYGQA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=env%2Creact%2Cstage-2&prettier=false&targets=&version=7.20.4&externalPlugins=&assumptions=%7B%7D)

![image](https://user-images.githubusercontent.com/95308384/201086591-7713a50b-14f2-4fd4-a514-a9a099a837f0.png)

class -> babel로 transfile 시 prototype으로 동작하는 것을 확인 가능하다. 자세한 내용은 [정리한 protptype](prototype.md) 확인

<br/>
<br/>

## 정리)

> ### Prototype 조작 지양
>
> 이미 JS는 많이 발전했다. 따라서 `빌트인 메소드`를 사용하는 것이 가장 안전하고 명시적이다.
>
> > 직접 만들어서 모듈화 => 배포 => NPM
>
> JS 빌트인 객체를 건들지말자

<br/>

---

Reference)<br/>
https://www.udemy.com/course/clean-code-js/learn/lecture/29892116?start=450#announcements<br/>

https://github.com/marpple/FxTS<br/>
https://github.com/marpple/FxJS<br/>

● 몽키 패치<br/>
https://all-dev-kang.tistory.com/entry/%EA%B0%9C%EB%B0%9C%EC%A7%80%EC%8B%9D-%EB%AA%BD%ED%82%A4-%ED%8C%A8%EC%B9%98Monkey-patch%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC<br/>
https://en.wikipedia.org/wiki/Monkey_patch<br/>
