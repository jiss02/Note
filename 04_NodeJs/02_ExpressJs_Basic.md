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

## 11강 - 미들웨어의 사용 body parser

미들웨어란 무엇일까? 개념을 확실히하기 어려우니 일단 다른 사람이 만들어 놓은 하나의 부품처럼 생각하도록하자.

### third-party middleware

남이 만들어 놓은 것을 뜻한다.

Express가 만들지 않은 미들웨어이다.

#### body-parser 미들웨어

`post`방식으로 정보를 전달받는 것은 양이 매우 많을 수 있다.

post 방식으로 넘어오는 데이터의 본체를 잘 가공해주는 것이 body-parser 미들웨어임.

> body: 웹브라우저 쪽에서 요청한 정보의 본체. 이를 설명해주는 것이 헤더.

```javascript
// 폼데이터의 처리는 해당 코드를 쓴다.
app.use(bodyParser.urlencoded({ extended: false }));
```

앱 use에 `bodyParser.urlencoded({ extended: false })`라는 코드를 호출하면 실행이 되면서 미들웨어가 들어오게된다.

>  바디 파서가 만들어내는 미들웨어를 표현하는 표현식이다.

main.js가 실행될때마다 위의 코드에 의해서 미들웨어가 실행된다. 

그 후 내부적으로 사용자가 전송한 post데이터를 분석해서 데이터를 가져온 다음에, 콜백을 호출하도록 약속이 된다.

> 첫번째 인자에 body를 자동적으로 넘겨준다.

## 12강 미들웨어의 사용 - compression

 데이터가 조금만 커도 수많은 사용자들이 접속하면, 바로 부담이온다.

(돈도 많이 들기도 한다)

이럴 때 필요한 것이 **압축**이다.

웹 서버가 웹브라우저에 응답할때,응답하면서 압축 방식을 알려준다.

그 후, 웹브라우저가 그 압축방식에 따라 데이터를 해제한다.





