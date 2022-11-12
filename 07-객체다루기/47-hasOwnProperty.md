# 47. Object.prototype.`hasOwnProperty`

`hasOwnProperty()` 메소드는 객체가 특정 프로퍼티를 가지고 있는지를 판별 후 `boolean` 값을 반환함.

모든 객체는 `hasOwnProperty`를 상속하는 `Object`의 자식이다. 해당 메소드는 객체가 특정 프로퍼티(argumnet)를 자기만의 직접적인 프로퍼티(prototype의 property는 해당되지 않음)로서 소유하고 있는지를 판별한다.

따라서 hasOwnProperty()는 객체의 프로토타입 체인을 확인하지 않는다.

<br/>

```javascript
const object1 = {};
object1.property1 = 42;

console.log(object1.hasOwnProperty("property1")); // true

console.log(object1.hasOwnProperty("toString")); // false

console.log(object1.hasOwnProperty("hasOwnProperty")); // false
```

<br/>
<br/>

### 프로퍼티의 존재 여부를 테스트

```javascript
o = new Object();
o.prop = "exists";

function changeO() {
  o.newprop = o.prop;
  delete o.prop;
}

o.hasOwnProperty("prop"); // true
changeO();
o.hasOwnProperty("prop"); // false
```

<br/>
<br/>

## 직접 프로퍼티와 상속된 프로퍼티의 비교

`직접 프로퍼티(prop)`와 `프로토타입 체인에서 상속된 프로퍼티(toString, hasOwnProperty)` 간의 차이점 비교

```javascript
o = new Object();
o.prop = "exists";
o.hasOwnProperty("prop"); // true
o.hasOwnProperty("toString"); // false
o.hasOwnProperty("hasOwnProperty"); // false
```

<br/>
<br/>

## 프로퍼티의 명칭으로서 hasOwnProperty 를 사용

JavaScript에서는 `프로퍼티 명칭으로서 hasOwnProperty를 보호하지 않`는다. hasOwnProperty 명으로 `변수 및 함수 선언 후 hasOwnProperty 호출 시 Object.prototype.hasOwnProperty이 정상 실행되지 않음`을 뜻한다. 따라서 올바른 결과를 얻기 위해서는 `Object.prototype.hasOwnProperty.call();`인 `외부 hasOwnProperty을 사용`하여야 한다.

```javascript
var foo = {
  hasOwnProperty: function () {
    return false;
  },
  bar: "Here be dragons",
};

foo.hasOwnProperty("bar"); // always returns false

// Use another Object's hasOwnProperty and call it with 'this' set to foo
({}.hasOwnProperty.call(foo, "bar")); // true

// It's also possible to use the hasOwnProperty property from the Object prototype for this purpose
Object.prototype.hasOwnProperty.call(foo, "bar"); // true
```

<br/>
<br/>

---

Reference)<br/>
https://www.udemy.com/course/clean-code-js/learn/lecture/29892150#questions/15997054<br/>
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty<br/>
