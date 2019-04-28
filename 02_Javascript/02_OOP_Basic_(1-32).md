# 3강

## 객체의 기본

멤버의 목록을 담는다고 해보자. 

단순히 목록을 담는다면 배열로도 충분하다. 

하지만 이런 멤버를 담을 때 **풍부한 설명*을** 원한다면? **객체**를 사용하자.



### 값 접근 방법

1. 객체.KEY  (`.`로 접근)
   - member.dev
2. 객체["KEY"] (`[]`로 접근)
   - member["dev"]

# 4강

 ## 객체의 반복문

### for 문

객체는**for in** 문을 통해 접근할 수 있다.

원소의 개수만큼 중괄호가 실행된다.

`for 변수 in 객체 {...}`

의 형태로 객체에 for문을 사용할 수 있다. 변수에는 순번에 해당하는 원소의 key값이 들어간다.



위와같은 for문을 쓸때, `객체.변수`의 형태는 쓰지않도록 주의하자. 

속성에는 변수가 들어갈 수 없기때문에 undefined가 뜰 것이다.

`객체["변수"]`의 형식으로 써주면 위와같은 위험을 해결할 수 있다.

# 5강

## 객체는 언제 쓰나요?

객체는 개발할 때 편리하게 여러기능을 사용하도록 그룹핑 해준다.

한마디로 연관된 것들 끼리 정리정돈을 해놓는 것이다.

# 6강

## 객체 만들어 보기

이미 JS자체에 들어있는 객체를 사용할 수 있지만, 우리가 객체를 만들어 사용할 수 있다.

한 번 객체를 만들어보자.

```javascript
var Mymath = {
    PI: Math.PI,
    random: function(){
        return Math.random();
    },
    floor: function(val){
        return Math.floor(val);
    }
}

```

> 함수가 어떤 객체에 속하면 메소드라는 말을 사용한다.

이렇게 관련된 함수와 변수를 하나의 객체에 담아 정리정돈 해보았다. 

객체는 서로 연관된 변수와 함수를 그룹핑을 하여 각각의 것에 이름을 붙여준것이다.

> 객체라는 수납상자에 관련 된 변수와 함수를 그룹핑하는 것

# 7강

## this

프로그램에서도 자기자신을 가리키는 대명사가 존재한다. 

그것이 바로 **this**이다!

```javascript
// 게임점수를 변수와 점수 합산 메소드
var kim = {
    name: 'kim'
    first: 10,
    second: 20,
    sum: function(f, s){
        return f+s;
    }
}
// 아 근데 아쉽다. 이미 kim객체는 내부에 담고 있는 값을 알고있는데..
// 좀더 간단하게 쓸 수 있는 방법이 없을까..
console.log(kim.sum(kim.first, kim.second));

//이렇게 하면 된다.
//근데 이것도 좀 아쉽다.. 객체의 이름이 바뀌면 번거롭게 바꿔줘야하기 때문이다.
var kim = {
    name: 'kim'
    first: 10,
    second: 20,
    sum: function(f, s){
        return kim.first+ kim.second;
    }
}

//이럴 때 this를 쓰자!
var kim = {
    name: 'kim'
    first: 10,
    second: 20,
    sum: function(f, s){
        return this.first+ this.second;
    }
}

console.log(kim.sum());
```

즉, `this`는 `메소드가 자신이 속한 객체`를 가리키는 **특수한 하나의 키워드**이다.

# 8강

## constructor의 필요성

객체를 찍어내는 공장이 있다고 상상하자.

프로그래밍적으로 객체를 찍어내는 공장을 만들면, 마치 쿠키틀로 쿠키를 찍어내듯 객체를 만들  수 있다.

```javascript
var kim = {
    name: 'kim'
    first: 10,
    second: 20,
    sum: function(f, s){
        return this.first+ this.second;
    }
}

var lee = {
    name: 'kim'
    first: 10,
    second: 10,
    sum: function(f, s){
        return this.first+ this.second;
    }
}
```

이렇게 객체를 하나하나 만드는 경우, 객체의 동작방법에 수정이 생겼을 때 모든 객체를 하나하나 수정해줘야한다.

이런 것이 매우 불편하니,

특정한 형식을 가진 객체를 찍어내는 공장을 만들어 객체를 양산해보자.

# 9강

## constructor의 사례

```javascript
// 해당 날짜에 대한 상태를 가진 date객체가 생성되는 것이다.
var d1 = new Date('2019-4-10');
console.log(d1.getFullYear());
```

- 시간을 알아내고 싶을때 사용하는 date()함수.

- 내부적으로 2019-4-10일 이라는 상태를 가진 객체가 하나 만들어진다.

- 객체의 설계도가 노출 되지 않는다. 하지만 우리는 만들어진 객체를 자유자재로 사용할 수 있다. 

앞에 **new**를 붙였을 때 **객체를 만들어서 우리에게 리턴**해준다는 것을 느낌적으로 알 수 있을 것이다.

이런식으로 **공장**을 만들면 편하게 객체를 생성할 수 있고, **수정할 것이 있을때** 공장부분을 수정하면 **전부 반영**이 되니 관리가 매우 수월해지는 것이다!

# 10강

## constructor 만들기

우리도 한번 공장을 만들어보자!

저번 강의의 코드를 다시한번 상기해보자. 

`new date()`의 형식인데, 호출하는 모양이 함수같더라!

모양이 함수같은 것이아니라 함수가 맞으며, **함수는 생성자도 되는 것**이다!

```javascript
function Person(name, f, s, t){
    this.name = name;
    this.first = f;
    this.second = s;
    this.third = t;
    this.sum = function (){
        return this.first+this.second+this.third;
    }
}

var kim = new Person('kim', 10, 20, 30);

console.log(kim.sum());
```

new라는 키워드를 붙이지 않고 그냥 실행하면 함수다. 

하지만 `new`를 붙여주면, 마치 마법같이 함수의 기능이 달라지는 것!

> 객체를 리턴하며 함수가 하나의 생성자(constructor)가 된다.

이런 기능을 통해, 객체의 틀을 바꾸면 해당 틀을 사용하는 모든 객체가 함께 변화되는 폭발적인 기능을 얻을 수 있다.

# 11강 

## prototype이 필요한 이유

프로토타입은 JS에서 매우 중요한 개념이다.

JS를 Prototype Based Language라고 부를 만큼 프로토타입은 JS를 지탱하는 기반이라고 볼 수 있다.



생성자는 쉽게 객체를 찍어내고 사용할 수 있게 해주며 변화를 용이하게 해준다. 하지만 생성자 내부의 메소드와 변수에게 변화가 생긴다면 골치가 아파질 것이다. 

이런 문제들을 통해 왜 프로토타입이 중요한지 알아보도록하자.



이전 강의의 코드에서 

```
this.sum = function (){
	return this.first+this.second+this.third;
	}
```

해당 부분은 꽤 아쉬움이 남는다. 

수많은 객체를 사용할 경우, 해당 함수가 매번 실행되는데, 이는 메모리에 부담을 줄 수 있기 때문이다.



다음 경우를 보자.

```javascript
function Person(name, f, s, t){
    this.name = name;
    this.first = f;
    this.second = s;
    this.third = t;
    this.sum = function (){
        return this.first+this.second
    }
}

var kim = new Person('kim', 10, 20);
// 이렇게 하나하나 객체의 sum을 바꾸면
// 생성자의 함수를 실행하고 kim객체의 sum메소드를 실행하는 비효율이 발생한다.
kim.sum = function({
    return 'modified: ' + (this.first+this.second);
})

console.log(kim.sum());
```

만약 Person 생성자를 사용하는 객체의 sum 동작을 바꾸게 된다면,

따로 kim객체의 sum 메소드를 선언하므로 생성자 안의 sum 메소드를 실행할 필요가 없어진다.

하지만 생성자 안에 메소드를 담아놓으면,

kim객체의 sum메소드를 나중에 따로 선언해줄 것임에도, 생성시에 생성자안에 존재하던 sum메소드를 실행하게된다 (불필요한 과정이다).

이러한 메모리낭비를 줄이기 위해 어떤 방법을 사용할 수 있을까? 

이 문제를 해결해주는 것이 바로 프로토타입이다.

# 12강

## prototype을 이용하여 재사용성을 높이기

```javascript
function Person(name, f, s, t){
    this.name = name;
    this.first = f;
    this.second = s;
    this.third = t;  
}

//Person 이라는 생성자에 공통적으로 사용되는 함수를 넣어주고 싶은 것임.
Person.prototype.sum = function (){
        return this.first+this.second
    }

var kim = new Person('kim', 10, 20);

console.log(kim.sum());
```

Person 생성자 내에 있는 sum함수를 밖으로 쏙 빼내어 프로토타입에 넣어주자.

Person 이라는 생성자에 공통적으로 사용되는 함수를 넣어주고 싶을 때 prototype(원형)에다가 넣어주는 것이다.

프로토타입에 메소드를 선언해줌으로서, 메모리의 낭비를 줄이고, 향후 다른 객체가 메소드의 동작을 변경할때도 불필요한 메소드의 실행을 막을 수 있으니 없어서는 안될 요소인 것이다.

__장점__

1. Person() 객체의 바깥에 있기 때문에 생성할 때 마다 실행되지 않는다.
2. 프로토타입으로 저장된 함수는 수많은 객체들이 함께 공유한다. 
   - 한번의 선언으로 여러개의 객체에 적용이 되는 것이다.

객체는 메소드를 실행할때, 

1. 해당 객체가 메소드를 가지고 있는지 먼저 찾아보고,
2. 객체 자신이 가지고 있지않으면 그 위의(부모의) prototype에 가서 해당 메소드가 있는지 찾는다.

함수는 웬만하면 **생성자 밖에 prototype을 사용**하여 써주자.

>  변수도 프로토타입으로 생성하는 것이 가능하다! 그러나 변수는 생성자 안에 넣는 것이 일반적.

__해당 질문에 스스로 답해보자__

프로토타입이란? 

이를 사용하지 않으면 메소드나 속성을 직접정의하면 어떤 비효율이 발생하지?

이를 해결하기위해선 어떻게하지?

# 13강 

## Classes

클래스는 파이썬, 자바, php 등의 언어들이 객체를 만드는 공장으로써 사용한다.

JS는 클래스를 지원하지 않았으나, 이를 도입함으로써 더욱 익숙하게 객체를 생성할 수 있게 되었다.

constructor function 을 대체할 수 있는 class를 살펴보자.

# 14강, 15강

## Classes의 생성, constructor function

```javascript
function Person(name, f, s, t){
    //객체의 초기 상태를 셋팅해준다.
    this.name = name;
    this.first = f;
    this.second = s;
    this.third = t;  
}
Person.prototype.sum = function (){
        return 'proto: ' + (this.first+this.second);
    }

// 공통부분
var kim = new Person('kim', 10, 20);
kim.sum = function(){
    return 'this: ' + (this.first+this.second);
}
console.log(kim.sum());
```

위와 아래는 같은 동작을한다. sum 메소드는 다음 강에서 구현해보자.

```javascript
class Person{
    //객체의 초기 상태를 셋팅해준다. 호출하지 않아도 자동실행된다.
    constructor(name, first, second){
        this.name = name;
        this.first = first;
        this.second = second;
    }
}

// 공통부분
var kim = new Person('kim', 10, 20);
kim.sum = function(){
    return 'this: ' + (this.first+this.second);
}
console.log(kim.sum());
```

클래스에서 메소드를 정의할 때, function이라는 키워드를 붙이지 않는다. 

클래스에서는 객체를 생성할때 초기상태를 지정하기위한, 객체가 만들어지기 직전에 실행되기로 약속된 함수가 있다. 

이는 바로 `constructor(){}` 함수이다.

메소드를 호출하지 않아도 객체가 만들어지며 자동으로 실행된다.

# 16강

## 메소드 구현

클래스 내의 메소드 구현은 크게 다르지 않다.



__1번__

클래스 바깥에 프로토타입으로 생성

```javascript
class Person{
    //객체의 초기 상태를 셋팅해준다. 호출하지 않아도 자동실행된다.
    constructor(name, first, second){
        this.name = name;
        this.first = first;
        this.second = second;
    }
}
Person.prototype.sum = function (){
        return 'proto: ' + (this.first+this.second);
    }
```

__2번__

클래스 내에 생성

```javascript
class Person{
    //객체의 초기 상태를 셋팅해준다. 호출하지 않아도 자동실행된다.
    constructor(name, first, second){
        this.name = name;
        this.first = first;
        this.second = second;
    }
 
    sum(){
        return 'proto: ' + (this.first+this.second);
    }
}
```

> sum은 같은 클래스에 속한 객체가 모두 공유하는 메소드이다.

# 17강

## 상속

상속이 필요한 이유?

객체의 틀이 있을 때 만들어놓은 객체의 틀과 비슷한 기능을 가지면서, 몇개의 객체에게만 새로운 기능을 추가하고 싶을 경우 사용하면 좋다. 

새로운 클래스를 생성하거나 (코드의 중복이 생김), 클래스 자체를 변경하는 것은 비효율적일 수 있다.

이런 문제는 상속을 통해 해결할 수 있다.

```javascript
class PersonPlus extends Person {
    avg(){
        return (this.first+this.second)/2;
    }
}
```

필요한 기능만 추가해주면 되므로 유지보수가 쉬워지며 코드의 중복을 피할 수 있다.

부모 클래스인 Person의 속성과 메소드를 모두 공유하므로 부모 클래스의 기능들 또한 마음껏 사용할 수 있다.

# 18강

## super

부모가 하는 기능은 그대로 하고, 부모가 못하는 기능은 자식이할 수 있도록해주는 키워드!

만약 세번째 인자를 추가하고 싶다면?

```javascript
class Person{
    //객체의 초기 상태를 셋팅해준다. 호출하지 않아도 자동실행된다.
    constructor(name, first, second){
        this.name = name;
        this.first = first;
        this.second = second;
    }

	sum(){
    	return (this.first+this.second);
	}

}

// 부모가 할 수 있는것은 super를 통해 가져오고, 자식 클래스가 수행할 추가적인 것만 적어주기.
class PersonPlus extends Person{
    constructor(name, frist, second, third){
        super(name, first, second);
        this.third = third;
    }
    
    sum(){
       return super.sum() + this.third;
    }
    
    avg(){
        return (this.first+this.second+ this.third)/3;
    }
}
```

### super()

super() 를 사용하면 부모 클래스의 생성자를 의미한다.

### super.method() or super.proprety

부모클래스의 속성이나 메소드를 호출하고 사용한다. 

# 19강

## Object inheritance

원래 다른 언어에서는 상속은 클래스끼리만 받으며, 객체의 기능은 이미 클래스로 정해져 있어 따로 상속을 받을 수 없다.

그러나 JS에서는 객체가 직접 다른 객체의 상속을 받을 수 있으며, 상속 관계를 바꿀 수 있다.

다른 객체에게 상속을 받고 싶을 때는 다른 프로토 타입을 연결하면 된다. 

이를 `prototype link`라고 한다.

`protorotype` 링크로 가리키는 객체를 `prototype object`라고도 한다.

# 20강

## \_\_proto\_\_

```javascript
var superObj = {superVal: 'super'}
var subObj = {subVal: "sub"}

subObj.__proto__ = superObj // 연결!

// 기존의 superObj 객체의 superVal 속성이 바뀌지 않고, sub 객체에 superVal 속성이 새로 생긴다.
subObj.superVal = 'sub'
```

처음 선언시 둘은 완전히 남남인 객체였지만, 이를 상속관계로 연결시켜줄 수 있다. 

**\_\_proto\_\_** 라는 프로토타입 링크를 통해 sub은 super의 자식이라는 것을 알려주었다.

`subObj.superVal`을 요청하면, subObj에 superVal이 있는지를 먼저찾고, 없으면 프로토타입링크를 따라 부모에게로 이동하며 superVal이 있는지 찾는다.

__`subObj.superVal = 'sub'`__

부모 객체에 있던 superVal이 변할 것이라 생각할 수도 있지만, 부모는 바뀌지 않는다.

자식 객체에 superVal 이라는 속성이 추가되어 값이 객체에 들어가니 헷갈리지 않도록하자.



언더바 proto는 표준적으로 권장하는 방법은 아니므로 사용을 지양하고 이와 같은 기능을 하는 대체제를 배워보도록하자.

# 21강

## Object.create()

```javascript
var superObj = {superVal: 'super'}
var subObj = {subVal: "sub"}

subObj.__proto__ = superObj;
```

 Object.create()를 통해 위의 코드를 바꿔보자.

기능은 동일하다.

```javascript
var superObj = {superVal: 'super'}
var subObj = {subVal: "sub"}

var subObj = Object.create(superObj); // 대체재!
```

새로운 객체를 만드는데 인자로 넘어온 객체를 부모로하는 객체를 만들어줘! 라고 하는 것.

그 후 새로운 속성이나 메소드를 추가하고 싶다면,

`subObj.subval = 'sub'` 와 같은 식으로 생성을 해주면 된다.

### TIP

`debugger;` 코드를 입력하면 자바스크립트이 동작이 멈춘다.

이 기능을 활용하여 여러가지 실험을 해보고, 객체의 상태가 어떤지를 확인하며 진행하면 좋을 것이다.

# 22강

## 객체 상속의 사용

```javascript
kim = {
    name: "kim"
    first:10, second:20,
    sum: function(){return this.first+this.second}
}
lee = {
    name: 'lee',
    first: 10, second:10}
lee._proto__ = kim;
// lee객체는 sum이라는 기능이 없지만 kim 객체를 상속받음으로써 사용이 가능하다.
```

```
var lee = Object.create(kim)
lee.name = 'lee';
lee.first = 10;
lee.second = 10;
```

 이라는 문장으로 대체가능하다. 

# 23강

## 객체와 함수

함수가 그냥 함수일 뿐만 아니라 함수를 호출할 때 new라는 연산자를 붙이면 생성자가 된다.

JS에서 함수는 함수이면서, 객체의 생성자도 될 수 있는 무궁무진한 요소이다.

# 24강

## call

함수의 this 값을 바꿀수 있는 함수.

```javascript
var kim = {
    name:'kim', first: 10, second: 10
}

var lee = {
    name:'lee', first: 10, second: 20
}
function sum(){
    return this.first+this.second;
}
sum.call();
```

`sum.call()`은 sum이라는 객체를 실행시키겠다는 것이다.

>  이를통해모든 함수는 객체라는 것을 알 수 있다.

모든 함수는 call이라는 메소드를 가지고 있고,

첫번째 인자로 객체를 주면 그 객체에 sum() 메소드가 추가되는 효과를 준다.

두번째인자부터는 호출하려는 함수의 인자값으로 들어간다.

# 25강

## bind

함수를 내부적으로 객체에 고정시키고 싶을 때 사용하는 함수.

call 함수처럼 첫번째 인자에 객체를 주고 두번째 인자부터 사용할 함수의 인자값을 넣어주면 된다.

하지만 call과의 다른점은, call은 실행할때 마다 sum안의 this가 가리키는 객체를 바꾸어주지만,

bind의 경우 실행되는 함수의 this값은 원하는 객체로 고정시키는 새로운 함수를 만들어내는 것이다. 

# 26강

## prototype vs __proto__

JS에서 함수는 객체다.

```
function Person(){}

는 아래와 같다.

var Person = new Function();
```

위의 코드에서 보듯, JS에서의 함수는 객체이기 때문에 property를 가질 수 있다.

### proto 와 prototype의 차이점

생성자 함수를 생성할 때 어떤 일이 일어나는지 알아야 차이점을 명확히 구분할 수 있다.

생성자 함수 생성하면,

생성자 함수 객체와 동시에 생성자 함수의 프로토 타입객체가 생성된다. 

이 둘은 서로 연결되어 있으며 constructor와 prototype이라는 속성으로 서로 연결된다.

A라는 생성자 함수를 통해 객체를 만들게 되면, 

객체안에 들어있는 \_\_proto\_\_ 속성은 A의 프로토타입 객체를 가리키게 된다.

proto속성은 부모 객체의 프로토타입 객체를 가리키는 하나의 링크이며,

실행하고자 하는 메소드나 변수가 해당 객체에 없으면 proto가 가리키는 부모의 프로토타입 객체로가 변수나 메소드가 존재하는지 확인하고 실행한다. 

즉 prototype은 constructor와 함께 생성되는 또 하나의 객체이고, \_\_proto__는 상속관계를 연결해주는 하나의 링크이다.

# 27강

## 상속 소개

객체와 객체가 직접 상속할 수도 있고, 클래스나 constructor함수를 통해서 상속을 할 수도 있다.

하지만 클래스로 상속하는 것이 쉽고 안전하니 이를 자주 사용하도록 하자.

```javascript
class Person{
    constructor(name, first, second){
        this.name = name;
        this.first = first;
        this.second = second;
    }
    
    sum(){
        return this.first + this.second
    }
}

class PersonPlus extends Person{
    constructor(name, first, second, third){
        super(name, first, second);
        this.third = third;
    }
    sum(){
        return super.sum() + this.third;
    }
    
    avg(){
        return (this.first + this.second + this.third)/3;
    }
}
```

클래스 내에서의 함수는 프로토타입 객체에 저장된 함수로,

해당 클래스에 속하는 객체들이 공유하는 것이다.

즉, 메모리 낭비가 덜하다!

# 28강

## 부모 생성자 실행

```javascript
function Person(name, first, second){
    this.name = name;
    this.first = first;
    this.second = second;
}
Person.prototype.sum = function(){
    return this.first + this.second
}

function PersonPlus(name, first, second, third){
    Person.call(this, name, first, second); // == super(name, first, second);
    this.third = third;
}
PersonPlus.prototype.avg = function(){
    return (this.first + this.second + this.third)/3;
}
```

PersonPlus의 초기화 부분에서 그냥 Person을 하면 안된다. 

new가 없으니 생성자가 아니라 함수처럼 호출 되는 것이다.

이럴때 `call`함수를 이용하여 중복되는 초기화 부분을 간단하게 줄일 수 있다. 

# 29강

## 부모와 연결하기

```javascript
function Person(name, first, second){
    this.name = name;
    this.first = first;
    this.second = second;
}
Person.prototype.sum = function(){
    return this.first + this.second
}

function PersonPlus(name, first, second, third){
    Person.call(this, name, first, second);
    this.third = third;
}
PersonPlus.prototype.avg = function(){
    return (this.first + this.second + this.third)/3;
}

//PersonPlus.prototype.__proto__ = Person.prototype;

var kim = new PersonPlus('kim', 10, 20);
    console.log(kim.sum());
```

`Person.call(this, name, first, second);` 는 person 을 호출한 것일 뿐, 서로 연결되어있지 않다.

따라서 kim객체에서 sum() 메소드를 실행한다고 해도 상속으로 연결이 안되어있으니 실행이 불가능하다.

이를 해결하기 위해 `PersonPlus.prototype.__proto__ = Person.prototype;` 코드를 통해 자식의 프로토타입이 부모의 프로토타입을 가리키도록 \_\_proto__를 사용하여 연결해주면 된다. 

object.create()를 통해 연결하는 방법은 아래에서 보도록 하자.

# 30강

## constructor 속성은 무엇인가?

객체가 누구로부터 만들어졌는지  알게해준다.

너의 클래스가 뭐야? 라고 물어보는 것과 비슷한 의미이다.


29강의 코드를 참고해보자.

PersonPlus를 따르는 kim이라는 객체를 만들고 kim.constructor를 하면 어떻게 될까?

PersonPlus를 가리킨다. kim에 constructor가 없어 프로토타입으로 가서 이를 찾고,

프로토타입에 있는 constructor를 따라 PersonPlus로 간다.

즉, kim.constructor는 kim이라는 객체를 생성한 생성자를 의미하는 것이다.

```
이런 것도 가능하다.
var d = new Date();
var d2 = new d.constructor
```

# 31강

## constructor 속성 바로잡기

```javascript
function Person(name, first, second){
    this.name = name;
    this.first = first;
    this.second = second;
}
Person.prototype.sum = function(){
    return this.first + this.second
}

function PersonPlus(name, first, second, third){
    Person.call(this, name, first, second);
    this.third = third;
}
PersonPlus.prototype.avg = function(){
    return (this.first + this.second + this.third)/3;
}

PersonPlus.prototype = Object.create(Person.prototype);

var kim = new PersonPlus('kim', 10, 20);
    console.log(kim.sum());
```

`PersonPlus.prototype = Object.create(Person.prototype);` 코드로 인해 PersonPlus의 prototype은 PersonPlus가 아니라 Person이 된다. 

완전히 replace되는 것이다.

위의 코드 부분은 밑에처럼 바꿔주면 되는데,

```
PersonPlus.prototype = Object.create(Person.prototype);
PersonPlus.prototype.constuctor = PersonPlus;
PersonPlus.prototype.avg = function(){
    return (this.first + this.second + this.third)/3;
}
```

이 코드도 완벽하지는 않다. avg 메소드를 만드는 코드가 

`__proto__`는 링크만 바꿔주면 되기때문에 간편하다.