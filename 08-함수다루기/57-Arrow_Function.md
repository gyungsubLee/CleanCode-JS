# 57. Arrow Function

함수를 표현식으로 간결하게 작성하는 화살표 함수가 존재한다.

이러한 화살표 함수를 맹목적으로 사용하는 경우, 예상치 못한 Error가 발생한다.

<br/>

## Case1 - Function 사용 시, `this`

```javascript
const user = {
  name: "LEE",

  // Arrow Funtion
  getNamOfAF: () => {
    return this.name;
  },
};

user.getNamOfAF(); // undefined
```

Arrow Function은 [lexical scope](https://developer.mozilla.org/ko/docs/Web/JavaScript/Closures#%EC%96%B4%ED%9C%98%EC%A0%81_%EB%B2%94%EC%9C%84_%EC%A7%80%EC%A0%95lexical_scoping)를 가져 상위 스코프의 객체를 참조한다.

위 예시 코드와 같이`method`의 Value에 `Arrow Function`으로 `this 조회` 시, `상위 스코프의 객체`인 전역객체를 조회하기 때문에 undefined가 출력된다.

<br/>

```javascript
const user = {
  name: "LEE",

  getName() {
    return this.name;
  },
};

user.getName(); // LEE
```

위와 같이 cosise Method로 작성 시, 정상적으로 해당 객체의 property를 조회한다.

<br/>
<br/>

## Case2 -Arrow Function 사용 시, `Arguments 사용불가`

```javascript
const user = {
  name: "Poco",
  getName: () => {
    return this.name;
  },
  newFriends: () => {
    const newFriendList = Array.from(arguments);

    return this.name + newFriendList;
  },
};

// user.newFriends('Jang', '장')
```

Arrow Function은 `일반적인 함수가 가지고 있는 모든 prototype을 상속하지 않`는다.. 그 중 대표적으로 `arguments`, `call`, `apply`, `bind` 등이 있다.

따라서 해당하는 prototype(`arguments`, `call`, `apply`, `bind` 등)을 사용 시, arrow function 사용은 지양해야한다.

<br/>

위 Case는 `Rest Parameter`를 통해 개선 가능하다.

```javascript
 . . .

newFriends: (...rest) => {
    return this.name + rest;
  },
};
```

<br/>
<br/>

## Case3 - Arrow Function, `생성자 함수` 사용 불가

```javascript
const Person = (name, city) => {
  this.name = name;
  this.city = city;
};

const person = new Person("poco", "korea");
```

생성자 함수를 Arrow Function으로 작성 시 Error가 발생한다.

물론 주로 class 키위드 사용한 문법을 통해 class 정의하여 생성자 함수를 작성하지는 않지만, `new` 키워드를 사용하는 함수를 Arrow Function으로 작성하는 경우도 Error가 발생한다.

<br/>
<br/>

## Case4 - Class에서 Arrow Function 사용 시 주의할 점

```javascript
class Parent {
  parentMethod() {
    console.log("parentMethod");
  }

  parentMethodArrow = () => {
    console.log("parentMethodArrow");
  };

  overrideMethod = () => {
    return "Parent";
  };
}

class Child extends Parent {
  childMethod() {
    super.parentMethod();
  }

  overrideMethod() {
    return "Child";
  }
}

new Child().childMethod();
new Child().overrideMethod();
```

<br/>
<br/>

## 정리)

### 주의하여 Arrow Function 작성해야 하는 Case들

> 1.  this
> 2.  Arguments
> 3.  생성자 함수, new 연산자 조합 불가
> 4.  Class에서 사용 시, 주의해야 할 점

화살표 함수를 주로 사용하되, 위와 같이 Error가 발생하는 edge Case들은 피해서 사용하자.

<br/>

---

Reference)<br/>
https://developer.mozilla.org/ko/docs/Web/JavaScript/Closures#%ED%81%B4%EB%A1%9C%EC%A0%80closure<br/>
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments<br/>
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes<br/>
https://www.udemy.com/course/clean-code-js/learn/lecture/30008166#announcements<br/>

<br/>

> Case4 이해 안됐음 -> 다시 학습 필요
