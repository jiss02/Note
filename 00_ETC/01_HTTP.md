# HTTP

웹 브라우저가 서버에게 요청하면 서버는 브라우저에게 응답한다. 이때 지키는 통신 규약이 http이다. 헤더를 통해서 요청 헤더와 응답 헤더를 볼 수 있다. 서버는 정보를 제공하면서 응답한 정보를 헤더를 통해 알려준다

## 리퀘스트(요청)

### 리퀘스트헤더

- 제일 먼저 나오는 첫번째 부분이 요청 행
- 중간이 리퀘스트 헤더
- 이둘을 합친게 리퀘스트 메세지 헤더
- 바디와 리퀘스트 메세지 헤더 사이에 빈라인을 넣어 이를 구분한다.
- 바디는 서버에게 주는 정보를 적는다. 

### get 요청파일

웹브라우저와 웹서버가 어떻게 통신할것인가? 

- get은 웹서버로부터 데이터 가져올때 사용하는 메소드.

### 리퀘스트헤더 분석

hostname이 꼭 필요하다. 요청하는 웹사이트의 웹서버의 주소를 적어야함. 

#### 포트번호

한대의 컴퓨터에는 여러개의 서버가 설치되어있을 수 있음.
포트번호에 등록된 웹서버를 의미하는 것!

#### 가상호스트

a서버가 a.com b.com c.com을 전부 호스팅 하는 것. 주소에따라 다른 데이터 접근 가능

#### 유저에이전트

웹브라우저의 다른 표현. 요청하는 웹브라우저가 어느 웹브라우저인지나 접속자의 브라우저, 운영체제등을 알 수 있다.  이를 통해 기계 접근시에 이를 감지하고 차단할 수 있음.

#### accept incodeing 

데이터 양이 많으면 서버가 압축하여 전송하고 브라우저
가 압축을 풀어서 처리한다. 이때 어떤 압축 방식을 지원하는 지를 적어놓는다.

#### if modified since

내가 가진 파일이 언제 받은게 마지막이라는걸 서버에게 알려준다. 뭐가 더 최신인지 비교해서 서버가 가진게 최신이면 브라우저에게 다시 전송해준다.

## 응답헤더

### status (첫째행) 

서버가 응답했을때 잘됐는지 안됐는지를 알려준다.

http버전/응답결과/이해하기 쉽도록 설명
(1,2,3,4×× informational responses)

### redirection

3xx: a.com으로 접속했을때 서버가 3××를 응답하면 웹브라우저가 다른곳으로 다시 이동한다. 
4××: 클라이언트쪽의 오류.
5××: 서버의 오류.

### content type

응답타입/언어(text/html)

### last modified

이 정보가 마지막으로 언제 수정되었는지.

## 요청헤더

웹브라우저가 요청 전에 요청서를 만들고 웹서버에게 전송할 정보가 있는경우 한줄 띄고 보내면 된다. 

## 응답헤더

응답 헤더후 한칸 띠고 본문 전체를 보내준다.

## https = ssl

http의 안전 버전. https를 사용하면 전송되는 내용응 가로채도 알 수 없다. 암호화가 되어있기때문에! 

## 캐시

성능향상 관심있다면 이를 공부하자. 한번 웹사이트에 접속해 내용을 다운로드 받았다면 다음에 또 다운받을 필요없이 이미 저장된걸 읽어 성능을 향상시킨다. 내용이 갱신되었을때 웹브라우저는 알아채지 못한다는 단점이 있다. 그래서 하는 것이 새로고침하여 캐시를 갱신함. 

## 캐시컨트롤 프라그마

사용자들은 캐시가 갱신되었다는걸 알수업다. 이를 위해 사용하는 것이 캐시컨트롤 프라그마. 캐시를 제어하는 테크닉이다. 애플리케이션 캐쉬같은 테크닉도 이런 목적.

## 개인화 (쿠키)

웹사이트 방문할때 장바구니 담기 로그인 등의 기록등을 웹브라우저가 기억하게하는데 이를 가능하게 하는 것이 쿠키. 저장된 쿠키값을 서버에 전송하여 사용자의 상태를 유지하고 사용자를 식별 할 수 있다. 

## 웹스토리지

쿠키보다 많은 정보를 저장하면서도 보안에 우수한 기술

## 프록시

중계서버. 중간 서버가 캐쉬를 대신하거나 보안과 관련된 공격을 막아주거나 적당히 사용자의 요청을 여러개의 서비스로 분산해주거나 하는 역할을 한다. 서비스가 복잡해지고 중요해진다면 이를 알아봐도 좋을 것이다

## 네트워크모니터링도구

- 개발자도구의 네트워크

- wireshark
	- 모든 네트워크 트레픽을 감시할 수 있게해준다. 배우기 어렵고 복잡하긴 하다. 오픈소스이고 강력한 도구.