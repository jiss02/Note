## Authentication

서비스를 이용하는데에 있어 내가 어느 정도의 권한이 있는지 알려주는(요청하는) 과정. 내가 어떤 유저인지 요청하는 과정이라 생각하자.

모든 사용자에게 동일한 권한을 주는 경우는 극히 드물다. 우리가 허가한 사용자, 또는 허가를 요청한 사용자만이 우리의 서비스를 사용할 수 있게해야한다.

따라서 권한관리는 매우 중요하다!

인증 요청이 들어오게 되면 `request.user`와 `request.auth`가 세팅이 된다.

__request.user__

인증이 성공한 경우 유저가 셋팅되는 공간.

__request.auth__

인증이 성공한 경우 유저의 권한이 셋팅되는 공간.

> 인증이 실패한 경우 AnonymousUser가 셋팅이 된다. (auth는 None)

### 전역설정과 뷰단 설정

전역설정은 settings.py에 넣어주는 것이며, 전역으로 디폴트 값을 설정해주고 싶을 때 사용하면 된다. 뷰단 설정은 공식문서를 참고하자. 

### BasicAuthentication

HTTP 자체 기본인증에 기반한 인증방식이다. HTTP는 기본적으로 헤더로 넘긴 ID와 PW를 base64 방식으로 인코딩 하는데, 이에 기반한 인증방식이라고 보면된다. 그러나 base64는 손쉽게 풀어낼 수 있기 때문에 단독으로 사용하는 것은 지양한다.

### TokenAuthentication

Basic 방법을 보완한 것이다. 인증요청을 보내면 그 사용자에게만 해당하는 유일한 key값을 발급하는 것이다.

> 해당 키값에 인증정보가 저장된다.

Token 헤더를 통해 인증이 수행된다. 이는 내용이 많으므로 추후에 다시보도록 한다.

### SessionAuthentication

장고의 디폴트 지정값이다. 장고의 미들웨어 중 session을 관리하는 것이 있는데 (`Sessionmiddleware`) 로그인이 될때마다 생성되는 세션을 관리한다. session이라는 변수에 session 정보가 저장이 되는데 이를 참조해서 인증을 수행한다.

### UserAuthentication

User정보가 다른 서비스에서 관리될 때 쓰이는 방식이다.

### httpie로 post해보기

이제 POST를 요청할 때 기존의 방식대로 하면 서버 에러가난다! 사용자의 이름과 비밀번호를 함께 전달해주어야 post 요청이 가능해진다.

```python
http --auth id:password --form POST http://127.0.0.1:8000/userpost/ title="안녕" body="인증"
```



## Permission

서비스를 어느정도 이용할 수 있는지에 대한 권한을 의미한다. View호출 시 가장 먼저 체킹되며 인증 정보를 기반으로 권한을 체크한다. `request.user`와 `request.auth`를 기반으로 권한을 체크하는 것이다!

permission 또한 settings.py 전역설정과 뷰단 설정으로 크게 두가지로 나누어진다.

### AllowAny (default)

인증된 요청이든 비인증 요청이든 모두 허용해준다.

### IsAuthenticated

인증된 요청에 대해서만 View 호출을 하겠다는 것이며, 등록된 사용자에게만 access 허용을 해주는 것이다.

### IsAdminUser

스태프 유저나 어드민에게만 허용해 준다는 것이다.

```python
User.is_staff == True # 일 때만 허용
```

### IsAuthenticatedOrReadOnly

비인증 요청에 대해서는 읽기만 허용하겠다

> 안전한 http method만 허용하겠다는 것이다.



## Token

다른 authentication의 한계로 Token을 많이 사용하는 추세이다. 유저별로 고유한 토큰을 발급하고 이에 기반하여 인증을 처리하는 것이다.

__수행과정__

1. username, password(유저별로)와 일대일 매칭되는 고유의 키를 발급
2. 발급받은 토큰을 API 요청에 담아 인증처리를 한다.

토큰인증은 세팅과 뷰에만 넣어준다고 되는 것이 아니라 `INSTALLED_APPS`에 `rest_framework.authtoken`을 추가해준 후 `migrate`를 해주어야한다.

토큰은 유저별로 일대일 매칭되는 고유의 식별값이라한 것에 힌트가 있다. 일대일 매칭이 된다는 것은 onetoonefield라는 것이기 때문이다!

> 실제로 authtoken의 모델을 보면 user와 원투원필드로 연결하는 부분이 존재한다.

유저 인스턴스가 생기면, 토큰을 생성해주어야한다!

### 토큰 발급 방법

#### rest_framework의 views.py

ObtainAuthToken을 이용하여 생성한다

#### Python 명령어로 생성

`python manage.py drf_create_token <username>`

`python manage.py drf_create_token -r <username>` (강제로 토큰 재발급)

### 토큰 획득

생성한 토큰을 획득하기 위해 url path를 지정해주자. 그 url에 대해 post 요청을 보냄으로써 획득한다.

