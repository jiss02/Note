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

```
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