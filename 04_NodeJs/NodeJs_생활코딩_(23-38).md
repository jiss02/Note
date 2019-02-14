# Node.js 23-30

## node.js로 파일목록 알아내기
수정, 추가, 삭제를 어떻게 반영할 것 인가

- ./: 현재 디렉토리
- fs.readdir

> 특정 디렉토리에 있는 파일의 목록을 배열로 만들어서 전달해준다.

## 함수
javascript에서 함수는 값이다.

- return을 만나면 함수는 바로 종료된다.
- 값(); 을 통해 실행

```
function name(parameter){
	...;
}
name(argument);
```

## 동기와 비동기
synchronous & asynchronous

- sync: return 값을 준다

```
var result = fs.readFileSync('syntax/sample.txt','utf8')
```

- async: 함수를 3번째 인자로 줘야함(callback). 
- 파일을 읽는 작업이 끝나면 3번째 인자 함수를 실행시킨다.

> 첫번째는 에러를 두번째는 파일의 내용을 인자로 공급해주도록 약속함.
> 3번째 인자 함수에 실행시킬 것을 입력하면된다.

```
fs.readFile('syntax/sample.txt','utf8',function(err,result){});
```

## Callback
인자를 callback으로 준다. 실행이 끝나면 해당 일을 수행하도록 callback을 인자를 주는 것이다.

```
var a = function() {
  console.log('A');

}

function slow(callback) {
  callback();
}

slow(a);

```

## Package manager
소프트웨어들을 생성, 설치, 업데이트, 삭제 등을 관리해주는 프로그램

- 언어나 운영체제별로 중요한 역할을 맡는다

__NPM__

- 대표적인 node.js의 매니저

__PM2__ 

- 프로그램이 꺼졌나 감시해준다.
- 파일이 수정되면 자동으로 프로그램을 다시 껐다 켜준다.
- pm2 start main.js
	- 실행중인 프로그램의 세부정보를 보여준다. 온라인인지, cpu는 얼마나 차지하고 있는지 등을 나타낸다.
- pm2 start main.js --watch
	- 계속 감시한다. 수정후 node를 껐다 킬 필요가 없다.
- pm2 monit
	- 프로세스를 전체적으로 볼수있도록 해준다. 
	- q로 나간다.
- pm2 list
	- 실행중인 프로세스의 리스트를 보여준다.
- pm2 stop main
	- 종료하고싶은 프로세스를 종료한다.
- pm2 log
	- 문제점을 화면에 보여준다.

## HTML form
사용자가 서버쪽으로 데이터를 전송하기 위한 것.

- textarea 태그: 여러줄을 입력할 수 있도록하는 것.
- form 태그: 입력한 정보를 어디로 보낼 것인가에 대한 주소가 필요하다. 
	
> from 안에 있는 각각의 사용자가 입력한 정보를 버튼을 눌렀을때, 액션 속성이 가리키는 서버에 쿼리스트링의 형태로 정보를 전송하는 html의 기능.

```
<!-- 쿼리스트링이 만들어진다. -->
<form action="http://localhost:3000/process_create">
  <!-- name은 이름을 주는 것이다. -->
  <p><input type="text" name="title"></p>
  <p>
    <textarea name="description"></textarea>
  </p>

  <!-- 전송할 수 있도록! -->
  <p>
    <input type="submit">
  </p>
</form>
```

## POST 방식으로 전송된 데이터 받기

웹브라우저가 form으로 정보를 전송할때 post방식으로 전송했다. post 방식으로 전송된 데이터를 nodejs 안에서 가져오려면 어떻게 해야하는 가.

- post방식으로 전송되는 데이터가 많을 수록,                                                    

## creatServer

nodejs로 웹브라우저가 접속할때마다 callback 함수를 node.js가 호출한다.

```
function(요청할때 보낸정보, 응답할때 웹브라우저에 전송할 정보)
```

## request.on

모듈의 parse 함수를 이용하여 정보를 객체화한다.

```
var post = qs.parse(body)
```

## redirection 
사용자를 다른 페이지로 튕겨버리는 것.