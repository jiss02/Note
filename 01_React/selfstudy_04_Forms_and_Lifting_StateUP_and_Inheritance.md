## Forms 

Form은 하나의 양식으로, 사용자로부터 입력을 받기위해 사용한다. 일반 HTML 태그는 

```html
<input name='name' value=something/>
```

의 형태로, value를 각각의 html태그들이 관리하는 형태이다.

하지만 React로 개발하는 만큼 JS코드(React)로 인풋태그들의 모든 value를 컴포넌트에서 관리할 수 있으면 데이터의 관리가 수월해 질 것이다. 이에 해당하는 개념이 `Controlled Component`이다.

### Controlled Components

value 리액트에게 통제받는 인풋 엘리먼트를 의미한다. controlled component의 경우 모든 데이터가 state에서 관리가 된다. 그렇기에 리액트에게 통제를 받는 다고 하는 것이다!

```html
<input value={this.state.name} name={'name'}/>
```

의 형태로 코드가 이루어진다.

> 인풋의 value 속성이 state에서 부터 오면 컨트롤 컴포넌트가 된다.



## Lifting State

여러 컴포넌트에서 공통으로 사용하는 state를 하나의 상위 컴포넌트로 끌어올려 관리하자는 것이다. 따로 사용하게 되면 값이 꼬이게 되고 헷갈리는 상황이 올 수 있으므로 하나의 컴포넌트로 끌어올려 통합 관리 함으로써 state를 관리하자는 경험이다.



## Composition

