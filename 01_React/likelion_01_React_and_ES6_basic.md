## React Native



## ES6

### Javascript?

HTML이 웹페이지의 뼈대이고 CSS가 앞에 보여지는 것이라면, JS는 웹페이지에 동적인 움직임을 부여해주는 역할을 한다고 보면된다.

### ECMA

웹브라우저가 어느정도 제어가 가능해지면서 JS에 더해 다양한 언어들이 등장하게 되었고, 웹브라우저마다 중구난방으로 방법이 생겨났다. 이를 하나로 묶어주는 역할을 한것이 ECMA이다. JS는 이 ECMA 스크립트의 부분집합이며, 이를 그냥 자바스크립트라고 부르기도 한다.

> JS와 다른언어를 포함하는 하나의 표준안이라고 생각하자.

ECMA Script의 줄여서 ES6, ES7이라 부르기도 한다.

> 버전별로 다르게 부른다.

### 함수 표현식 방식 (함수도 객체에 기인한다)

```javascript
const a = function(a, b){
	reutrn a + b;
}

// 이외에도 여러가지가 있으나 제일 외우기 쉬운것으로 쓰다가 익숙해지면 더 보도록하자.
```

#### 화살표 함수

```javascript
const arr_fun = (a, b) => { return a+b }
```

__let__

es6 부터 생겨난 문법으로, 지역변수를 선언하는 것이다. 기존의 var는 전역변수이다.

__const__

상수이며, 주솟값의 변경은 되지 않는다. 웬만하면 const를 많이 사용하도록하자!

> 배열의경우 원소의 변경은 허용해준다.

### 상속

기존 JS에는 prototype을 통해 상속을 했다면 es6부터 class라는 개념이 등장했으니 이를 사용하도록하자.

```javascript
class MyClass {
    constructor(name){
        this.name = name
    }
    method(){
        
    }
}

class MyClass2 extends ParentClass {
    construct(name){
        super(name)
    }
    method(){
        
    }
}
```



## React

### JSX

자바스크립트 XML의 줄임말이다. 리액트에서 사용하는 문법이라고 생각하자. 새로운 표현식으로 아래와 같은 코드를 가능하게 해준다.

```javascript
const element = <h1>Hello!</h1>
```

즉 자바스크립트와 HTML태그가 결합된 것이라고 보면 된다. 

> 태그를 무조건 닫아주어야한다!

__react element__

```javascript
const App = () => { //App이 하나의 컴포넌트. 이를 모듈화를통해 index.js에서 사용이 가능하다.
	return (
		<div>
        hello!
        </div>
	);
};
```

의 코드가 존재할 때, `<div>hello!</div>`가 바로 하나의 엘리먼트이다.

이 리액트 엘리먼트가 모여 컴포넌트가되고, 컴포넌트가 모여 하나의 앱이된다!

> 컴포넌트인 것을 알려주기 위해 대문자로 시작한다. 

함수뿐만 아니라 클래스로도 컴포넌트 생성이 가능하다!

```
class App extends React.Component {
	render() {
		return (
		<h1>
			hello!
		</h1>
		);
	};
};
```



