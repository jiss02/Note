## 5.1 회원가입 로그인 로그아웃 이론

### 5.1.1 import 해야하는 것

```python
from djagno.contrib.auth.models import User
from django.contrib import auth
```

### 5.1.2 회원추가

```python
User.objects.creat_user() 
create_user(username, password)
```

User의 쿼리셋 objects의 메소드 create_user()를 사용하여 새로운 회원을 추가해 준다.

인자는 유저네임과 비밀번호를 치면 끝이다.

### 5.1.3 로그인

```python
auth.authenticate() # 등록된 회원인지 확인
auth.login(request, user) # 로그인
```

### 5.1.3 로그아웃

```python
auth.logout(request) # 로그아웃
```

### 5.1.4 http Method

정보를 주고받는 방식, method를 나눈이유?

**GET**

메소드를 지정하지 않으면 GET방식이 디폴트이다. 

하지만 GET방식은 url로 통신하며, 입력한 정보가 url에 노출된다.

하지만 계좌나 아이디 비밀번호와 같은 개인적 정보까지 url에 노출되는 것이 단점이다.

**POST**

url로 개인정보가 직접노출되지 않는 POST방식이 존재한다.

get방식 처럼 url로 드러나는 것이 아니라 숨겨져서 전송된다.

**그외의 메소드**

- 수정: PUT
- 삭제: DELETE
- 생성: POST
- 조회: GET

회원 가입은 내 개인 정보를 생성하는 것이므로 "POST"로 보내면 된다!



## 5.2 실습

`{% csrf_token %}`

정보보안을 위한 난수 생성기.

csrf 공격을 막기 위한 수단이다.

### 5.2.1 로그인

```python
auth.authenticate(req, username = username, password = password) # 등록된 회원인지 확인
```

데이터 베이스에 회원 정보가 있는지 확인한다.

회원인지 아닌지를 판가름 해주는 역할이다.



## 5.3 Pagination 이론

만약에 우리가 쓴 글이 지금처럼 밑으로 쭉 내려간다고 했을 때,

만약 글이 천개가 되고 만개가 된다면 아마 스크롤 하는 것에 한계가 올 것이다.

이를 위해 우리가 해야하는 것은 **페이지 별로 글을 끊는 것**이다.

### 5.3.1 어떻게 구현해야 할까?

Template과 View를 건드려주어야 할 것이다! 

페이지 이동 등을 보여주어야하므로 => Template

3개의 블로그 객체를 한 페이지에 담아서 한 페이지 씩 출력해줘! => Views

```python
from django.core.paginator import Paginator
```

1. 어떤 객체를 한페이지당 몇개 씩 담아 페이지로 띄울 것인지 결정 (마치 식빵뭉치를 자르는 효과)
   - Paginator(어떤 객체를, 한페이지당 몇 개씩)
2. 이젠 전체 데이터가 아닌, 페이지를 한 단위로 갖고 놀아야한다. (빵 한조각)
   - .get_page(페이지번호)
3. 페이지 한조각 (빵 한조각)을 html에 담아 띄우면 된다.

__Paginator vs Page__

Paginator는 식빵조각들을 모아놓은 것 (여러 페이지가 모여있는 것)

Page는 식빵 한조각을 가져온 것

우리는 Page객체를 얻기위해 Paginator를 이용할 것이다.

### 5.3.2 페이지 번호는 어떻게 알까?

```python 
page = request.GET.get('page')
# page변수 안에는 request를 보낸 페이지 번호가 담긴다.
```

request 객체에는 사용자가 보낸 총체적인 정보가 담겨있다.

어떤 데이터를, 어디서 어떤 페이지를 보냈는지 등등이다.

여기서 `request.GET`은 GET방식으로 보낸 내용을 지칭하게 되는 것이다.

`get('key')`의 형태는 딕셔너리형에 대해 key값을 인자로 주면 value를 반환하는 형태로,

key값이 'page'인 것의 value, 즉 페이지 번호를 뱉어주는 것이다.

```python
dict = {'Name': 'Zabra', 'Age': 7}
print "Value : %s" %  dict.get('Age')
```



## 5.4 Faker

pip package로 웹사이트를 만든 후 가짜 데이터들을 넣어 한번 볼 수 있게 해주는 것이다.

즉, 가짜데이터를 생성할 수 있는 능력을 가진 클래스이다.

```
from faker import Faker

myfake = Faker()

# Faker의 메소드를 통해 어떤 종류의 가짜데이터를 뽑아낼지 결정가능

myfake.name()
myfake.address()
myfake.text()
myfake.state()
myfake.sentence()
myfake.random_number()

# 한국어로 하고 싶다면

myfake = Faker('ko_KR')

```

만약 몇번을 출력해도 값이 유지되길 원한다면,

그때 사용하는 것이 Seed파일이다.

`myfake.seed(Seed번호)`의 형태로 사용한다.

seed번호는 각각의 거짓 데이터에게 부여되는 숫자라고 보면 되며,

지정해준 번호에 해당 거짓데이터가 들어가게 되어 seed번호를 바꾸지 않는 이상 같은 데이터가 출력된다.