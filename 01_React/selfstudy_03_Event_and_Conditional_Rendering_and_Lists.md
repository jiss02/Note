## Event

하나의 특정한 사건이다. 예를 들어 사용자가 버튼을 눌렀다고 생각해보자. 그럼 이는 하나의 `버튼을 클릭하는 사건`이 되는 것이다.

 ### Event Handler

이벤트가 발생하면, 이를 처리하는 역할을 하는 함수이다. `Event Listener`라고도 부르는데, 이벤트가 발생할 때 까지 가만히 듣고있다가 이벤트가 발생하면 이를 처리하기 때문이다.  



## Conditional Rendering

**조건에 따른 렌더링**을 의미한다! 조건에 맞으면 A라는 정보를 보여주고, 맞지 않으면 A라는 정보를 숨기는 경우를 이야기 한다.

```react
function CheckVip(props) {
	const isVip = props.isVip;
    // 조건에 따른 렌더링 코드
    if (isVip) {
        return <VipInfo/>;
    }
    return <VipInfo/>;
}
```

### Element Variable

변수 안에 리액트 엘리먼트가 담겨있는 경우를 의미한다.

### Inline Conditions

`&&`를 사용하여 조건적으로 렌더링 하는 것을 의미한다. 만약,

`true && info`이면 info가 렌더링 되고,

`false && info`이면 info가 렌더링 되지 않는다.

아래의 코드를 통해 간단히 살펴보도록하자.

```js
{ assignment.length > 0 &&
	<p>
		oh You still get {assignment.length} of assignment.
	</p>
}
```

만약 과제가 남아있다면 True가 되어 p 태그가 출력되고, 과제가 없다면 아무것도 출력되지 않을 것이다.

> if else 처럼 사용하고 싶다면 **삼항 연산자**를 사용하면 된다.

### 컴포넌트의 렌더링을 막고싶은 경우

**null**을 리턴해주면 된다. 사용자에게 경고를 주는 경우를 예로 들어보자. 경고가 있으면 경고창을 렌더링하고, 만약 경고가 없다면 딱히 렌더링 할 내용이 없으므로 `return null`을 통해 렌더링하지 않을 수 있다는 것이다.



## Lists

JS의 변수나 객체들을 묶어놓은 것이다. `Array(배열)`이라고 할 수 있으며 리액트에서는 이 배열을 사용하여 여러 엘리먼트를 렌더링할 수 있다!

많은  Item들을 손쉽게 렌더링 할 수 있게 해주며, 아래의 코드처럼 사용하면 유용하다.

```
const element = ['apple', 'banana', 'mango']
const items = element.map((fruit) =>
	<li>{fruit}</li>
	);
```



## Key

`중복되지 않는 고유한 값`이다. key는 해당 elements 사이에서만 고유한 값이면 된다! 즉, 현재 속해있는 리스트 내에서만 고유한 값을 가지면 되며, 다른 리스트와 키가  중복되는 것은 상관없다. 인덱스로 Key값을 설정해도 되지만 **index는 고유하지 않고 수시로 변하므로** 권장하지는 않는다.

리액트에서 Key의 존재는 어떠한 아이템이 바뀌고 추가되고 삭제되는, 즉 변화가 일어나는 것에 대해 큰 도움이 된다. 변화가 되는 부분만 인식하고 해당 부분만 렌더링 할 때 고유한 Key 값이 있다면 훨씬 수월해진다는 것이다!

키는 props로 전달되지 않으므로, 별도로 사용하고 싶다면 별도의 프로퍼티에 담아주면 props로 전달이 된다. 아래에 코드는 예제이다.

```react
<ListItem
	key={lists.id}
	id={lists.id} // 따로 넘겨줌
	/>
```

또한, JS의 함수인 `map`에 들어가는 element는 key가 필요하며, 만약 key를 입력해주지 않으면 index가 기본값으로 들어가게 된다.

> map에 들어가는 엘리먼트(or 컴포넌트)에 key 속성을 주어야한다는 것이다.