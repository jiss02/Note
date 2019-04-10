# Web3 - Express

## 3, 4강 - Hello World

Express는 모듈이므로 require를 통해 가져와야한다.

```javascript
const express = require('express')
const app = express() 
// express는 함수구나.
// 애플리케이션 객체만 담길 수 있구나.

app.get('/', function(req, res) {
  res.send('Hello World!');
});

// listen 메소드에 3000이 들어오면 3000포트에 리스닝을 하게 되고, 
// 이를 성공하면 콜백을 실행한다.
app.listen(3000, function(){
  console.log('Example app listening on port 3000!');
});
```

`const` 는 상수를 의미한다.

- 바뀌지 않으며, 앞으로 다른 값이 들어올 일은 없다! 라고 얘기해주는 것이다.

`get` 함수는 route, routing 이라고 많이 한다.

- 사용자들이 경로를 따라 들어올때, 경로마다 적당한 응답을 해주는 역할이다.
- get이 패스를 전달 받음으로써 routing을 하고 있는 것이다.

## 5강 - 홈페이지 구현

`express`가 제공하는 `route`를 이용하게되면,  각각의 처리하는 부분의 response와 require를 따로 모아놓을 수 있어 가독성이 좋아진다. 

## 6강, 7강, 8강, 9강, 10강 - 상세페이지 구현

**최근의 트렌드는 쿼리스트링을 자주 사용하지 않는 것! (2018 기준)**

`?id=html` 이던걸, `/html`로 오도록 하는 것이다.

```javascript
// pageId(마크)가 들어오면 req.params객체에 담기게 된다. 
app.get('/page/:pageId', function(request, response){
  return response.send(request.params);
});
```

`url path` 방식으로 파라미터를 전달하는 것을 처리하는 routing 기법을 살펴보기 시작한것이 가장중요하다.

즉 Express 는,

**Path** 별로 어떻게 응답할 것인가와

get 방식, post 방식으로 접속했을 때 어떻게 구분하여 응답할지를 아는 것이 시작이다.