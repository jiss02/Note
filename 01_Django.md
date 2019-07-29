# 01_1주차

## 1.1_기본환경 셋팅

프로젝트를 위해 장고를 설치할 때에는, 가상환경을 만들어 설치하자.

하나의 통안에 담는다고 생각하는 것이 좋다! 다른 프로젝트에는 영향을 미치지 않도록 하기 위함이다. 

> 여러 프로젝트를 수행하며 프로그램들이 꼬일 수 있거나 무엇을 설치했는지 헷갈릴 수 있기때문이다.

1. `python -m venv <name>`
2. `source <name>/Scripts/activate`
3. `deactivate` (가상환경 종료)
4. `pip install django`

## 1.2_hello world 이론

Django는 어떤 과정을 거치며 데이터가 처리될까?

- 데이터가 여러 파일들 사이에 티키타카로 전송된다.

### 1.2.1_어디서 티키타카를 하는가?

__장고를 설치하고나서...__

먼저, 처음 장고를 시작하면 장고 프로젝트를 먼저 생성해줘야 할 것이다.

- `django-admin startproject <name>` 명령어를 실행하면 여러 프로젝트 폴더들이 생성된다.
- manage.py로 서버를 돌린다고 생각하면 된다.
- project이름으로 된 폴더안에는 `settings.py`, `url.py`가 들어간다.

`python manage.py runserver` 명령어로 서버를 구동한다.

__APP__

프로젝트의 구성 단위. 앱이 프로젝트의 작은 부분이며, 앱들이 모여 프로젝트를 이룬다.

`python manage.py starapp <app name>` 명령어로 app을 실행한다.

- 앱 이름으로 된 여러개의 폴더가 생긴다.

_앱 이름으로 생성된 여러개의 파일과 프로젝트 파일의 파일들끼리 **티키타카**를 진행한다!_

### 1.2.2_어떻게 티키타카를 하는가?

__templates 폴더__

일단 방법을 알기전에, 앱 폴더 안에 **templates**폴더를 만들어 줘야한다.

앱을 하나 만든다고해서, 프로젝트 폴더가 이를 알 수 는 없다.

따라서 사용자가 만든 앱을 알려줘야하는데, 프로젝트 폴더의 settings에 알려주면 된다.

이 폴더안에는 유저에게 보여질 화면(html)을 담으면 된다.

> 유저에게 보여지는 화면이라고 보면 편하다.

__views.py__

유저에게 보여질 화면이 언제, 어떻게 처리될지 알려주는 **함수**를 작성한다.

상황에 따라 다르게 처리되는 함수를 작성하는 것이다.

> 어떤 링크로 들어오면 이 html을 띄우세요~ 

__url.py__

내가 만든 html이 어떤 url을 입력했을 때 뜨게할지를 결정한다.

__정리__

1. 프로젝트 만들기
2. 프로젝트의 작은 부분인 앱만들기
3. 만들어진 앱을 연결하라고 `settings.py`에 알려주기 (프로젝트와 앱연결)
4. `템플릿폴더` 만들어 유저에게 보여줄 페이지 입력
5. `views.py` 에서 만들어진 html이 어떤 상황에서 어떻게 처리될지 알려주는 함수
6. `url.py`에서 해당 html파일과 url을 연결해준다.

## 1.3_hello world 실습

> 포트번호: 8000 내컴퓨터를 의미한다.

__서버실행__

서버를 실행하고 나면 `db.sqlite3`이라는 파일이 생성되는데, 이는 db를 다루는 파일이다.

__프로젝트와 앱 연결하기__

프로젝트의 settings.py에 `myapp.apps.Myappconfig`를 입력해준다.

myapp의 apps파일에있는 MyappConfig 객체를 끌어와 달라!

> 앱이름.apps.앱이름Config

__views.py 작업하기__

```python
# 언제 어떤상황에서 사용할지 알려주자.
# 요청이 들어오면, home이라는 html을 내보내줘.
def home(request):
    return rendor(request, 'home.html')
```



__url.py에 작업하기__

```python
# url설계를 하자. 어떤 url이 들어올때 무엇을 실행할지.

from django.contrib import admin
from django.urls import path
# views.py에 쓰고자하는 기능이 들어있으니 임포트해주자.
import myapp.views

# 새로운 url넣어주자.
urlpatterns = [
    # /admin을 하면 저 url을 띄우세요!
    path('admin/', admin.site.urls),
    # 아무런 슬래쉬가 없는 사이트. 즉 홈이다.
    path('', myapp.views.home, name='home')
]
```

path (라우터, 실행시킬기능, 경로이름)

라우터에는 `/`뒤에 어떠한 조건이 붙었을때 무엇을 실행시킬지 알려주는 인자이다.

> 경로이름을 함수와 동일하게 짓도록하자. 그게 편하다.

# 1.5주차

## MTV 패턴

정보의 티키타카로 작동한다. == MTV 패턴.

- Model: DB를 다뤄주는 역할. 데이터를 뒤적뒤적한다.
- Template: 보여지는 화면
- View: 데이터가 어떤 상황에서 어떻게 처리되는지 모여있는 장소

각자 독립적으로 임무를 수행하며 장고 전체를 구동시킨다.

> 유지 보수가 편하다.

MVC 패턴을 차용한 방식이다. `C는 controller로 중간관리`를 하며, 여기서의 `View는 사용자에게 보여지는 부분`을 담당한다.

한마디로, MVC패턴의 view와 MTV패턴의 view는 다르다는 것이다. 헷갈리지 않도록 주의하자.

__tip__

html에서 장고 문법은 꺽쇠`{{ }}`안에! 

# 02_2주차

## 2.1_wordcount 이론 _ 1

__복습__

장고 프로젝트를 만들고, 프로젝트를 이루는 구성단위는 앱이다. 

1. 프로젝트와 앱을 만들면 
2. 프로젝트의 `settings.py`에 앱이 만들어 진걸 알려주고
3. 앱에 `templates` 폴더를 만들어 사용할 html을 넣어줄 준비를 하고
4. `html`을 넣어준뒤
5. 템플릿이 어떤 상황에서 어떻게 표시될지를 앱의 `views.py`에서 함수를 정의해주고
6. 프로젝트의 `url.py`에 들어가서 해당 템플릿이 표시될 url도 만들어 주면 된다.

## 2.2_프로젝트 스케치

1. 어떤 정보를 보여줄지 틀을 잡자.
2. 우리가 만들어야할 HTML 파일이 무엇이고 몇개인지 정하자.
3. 각각의 html이 무슨기능을 할지 서술해보자. 
4. 정보를 어떤 상황에서 어떻게 알려줄지 처리하는 함수를 정리해보자.
5. 그리고 각 페이지에 맞게 url을 구상해주면 간단한 전반적인 스케치 과정은 끝난다.

## 2.3_템플릿 언어

HTML 안에 쓰는 장고 제공언어. 장고 문법을 html에서 사용할 수 있다!

### 2.3.1_템플릿 변수

`{{ python_var }}` 해당 파이썬 변수를 html 파일에 담아 출력해라!

### 2.3.2_템플릿 필터

템플릿 변수에 추가적인 속성 및 기능 제공

`{{ python_var | filter }}`  의 형태로 사용한다.

__예시__

`{{ python_var | lower }}`  :  변수를 소문자로 출력하라!

### 2.3.3_템플릿 태그

html에서 파이썬 문법사용, url 생성등의 기능을 제공한다.

`{% tag %}...태그내용...{% endtag %}` 의 형태로, 

마치 하나의 태그처럼 닫는 태그도 써주어야 한다.

__url 생성__

`{%  url 'url_name(path name)' %}` 의 형태로,

url 태그에 해당하는 위치에 url을 생성해준다.

### 2.3.4_템플릿 상속

## 2.4_wordcount 실습

### render 함수에 대하여

`render(request, 'main.html', ...)` 의 형태로 첫번째 인자는 주로 리퀘스트(요청)가 들어오며,

두번째 인자로는 어떤 템플릿을 띠워줄 것인지 지정해준다.

세번째 인자로는 사전형 자료, 객체를 담아 변수를 전달해 줄 수 있다. 

# 03_3주차

__학습목표__

Model 에 데이터를 어떻게 담을 것인가

Model의 데이터를 어떻게 view로 넘길 것인가

그것을 어떻게 화면에 띄울 것인가

## 3.1_model & admin 이론

### 3.1.1_Model

데이터베이스를 다뤄준다.

우리는 `model.py`에 우리가 원하는, 가공하고자 하는 데이터를

종류가 무엇이고 어떤식으로 데이터가 처리되길 원하는지 **class**의 형태로 알려주면된다.

우리가 사용하고자 하는 데이터의 틀(형식)을 잡아 정의해주면 된다.

> 일기라고 치면 >>짧은글(제목), 시간, 긴글<< 의 틀을 가질 것이다.

```
class 블로그글:
	짧은글
	시간
	긴글
```

`model.py`는 데이터를 만드는 공장이고,

Class는 객체를 편하게 찍어내기위한 틀이다.

__팁__

데이터 베이스는 장고와 별개이며, setting.py에서 등록해줄 수 있다.



### 3.1.2_데이터베이스와 장고

장고는 데이터 베이스에게 model.py안에 어떻게 생긴 데이터를 처리하기로 했는지 알려주면 된다!

그 명령어는,

```
# 데이터베이스에게 모델을 만들거라고 알려주는 과정
$ python manage.py makemigrations
# 실제로 데이터베이스에 우리가 만든 것을 적용하는 과정
$ python manage.py migrate
```

이다.



### 3.1.3_어드민 계정 생성

위의 과정을 마친 후, 어드민 계정을 생성해 주어야 하는데, 

`$ python manage.py createsuperuser` 명령어를 통해 생성이 가능하다.

그 후, `admin.py`에 어떠한 데이터를 처리할 것인지를 등록하자.



### 3.1.4_정리

1. Models.py 안에 어떤 종류의 데이터를 처리할지 Class로 정의
2. DB에게 알아듣게끔 두개의 명령어 입력하기
3. admin 계정 만들기.
4. admin.py에 활용할 데이터 등록

> 데이터베이스에 어떻게 생긴 데이터를 집어넣을지 정의하고, 거기에 admin권한으로 데이터를 집어 넣는다.

## 3.2_model&admin 실습

데이터베이스에 있는 자료를 template에 띄우고 싶다면 어떻게 해야할까?

바로 띄울 수는 없을 것이다.

그러므로 중간 역할을 하는 view를 거쳐야 한다!

어떤 데이터가, 어떻게 처리될지를 함수로 정의해주자.

아래와 같은 함수를 정의했다고 해보자. 

Blog는 models.py에서 만든 무언가의 객체틀이라고 보면 된다.

```python
def home(request):
    # 블로그 안에있는 객체를 담아주자.
    # 모델로 부터 객체 목록을 전달받는 것이다.
    blogs = Blog.objects # 쿼리셋
    return render(request, 'home.html', {'blogs':blogs})
```

__쿼리셋__

모델로부터 전달받은 객체 목록을 의미한다.

쿼리셋을 기능들을 처리하거나 정렬하도록 해주는 것이 **메소드**이다.

### 3.2.1_쿼리셋 메소드

데이터를 늘 전체만 찍어보는 것이아니라, 

일부만 찍어보고 싶을 수도 있고 정렬을 해보고 싶을 수 도 있을 것이다. 

이럴 때 사용하는 것이 쿼리셋이다!

한마디로 쿼리셋 메소드는, **쿼리셋을 활용할 수 있게 해주는 것**이다.

#### 활용 방법

`모델이름.쿼리셋`.메소드 == `model.objects.method`

# 04_4주차

## 4.1_pk, path converter, get_object_or_404

### 4.1.1_what to do?

1. 글자수 제한
2. ...more 링크
3. detail 페이지로 이동하기

만약 우리가 게시글을 자세히 보고싶어 더보기 버튼을 눌렀다고 하자.

그렇다면 detail 페이지로 이동하게 될텐데,

게시글의 수만큼 이에 대응하는 detail 페이지를 만들 수 있을까?



만약 1억개의 게시글이 있다면, 1억개의 디테일 페이지가 있을텐데..

만약 디테일 페이지를 수정해야할 일이 생긴다면.. 정말 끔찍할 것이다.



이 문제를 해결하기위해 객체마다 번호를 부여하고,

하나의 디테일 페이지에 그 번호에 해당하는 객체를 넣어 띄워주는 방식을 취할 수 있다.

하나의 디테일 페이지라는 틀에, 알맞은 객체를 그때그때 갈아끼워주는 것이다.



x번째 객체를 사용자가 요청하면, 우리는 그에 해당하는 객체를 보여줘야한다.



#### 4.1.2_url 설계

우선 사용자가 요청과 함께 전달하는 객체의 번호를 받을 수 있도록 url을 설계하자.

`path('detail/<int:detail_id>', view.py의 함수, url 이름)`

`detail/객체번호` 의 형태로 url을 받은 것인데, 형태가 좀 이상하다.

이가 바로 path converter이다.



#### 4.1.3_path converter

`<type:변수이름>`의 형태를 가진다! 

위에서의 변수이름은 detail_id로, 

이는 views.py의 함수에 인자를 넘겨줄 때 어떤 이름으로 넘겨줄 것인지를 적어주는 것이다.

그러므로 뷰의 함수가 인자를 전달받을때, 

request인자와 함께 detail_id를 인자로 받아야 할 것이다.

## 4.2_pk, path converter, get_object_or_404 - 2

이용자가 x번 객체를 가져다줘! 라고 요청을한다면,

url을 타고 우리의 장고에 들어오게 될 것이다.



우선 path converter를 통해 url을 설계해주자.

어떤 형태의 데이터를 url로 받을지 정의해주고,

함수에 인자를 어떤이름으로 넘겨줄건지를 정의해주면된다.



(이클래스안에서 가져올건데, 몇번째 값을 가져와줘)

## 4.3_글쓰기 구현하기

### 4.3.1_tip

#### url

url은 그냥 무조건 어떤 페이지를 만들어야 하는 것이 아니라, 

이런 기능을 실행하라고 알려주는 것이다.

함수 실행시키고 싶어서 url을 만든 것이다!

### 4.3.2_페이지를 띄우는 함수 구현

단순히 페이지를 띄우기만 하는 함수이다.

```python
def new(request):
    return render(request, 'blog/new.html')
```

### 4.3.3_글쓰기 구현

입력 받은 것을 데이터 베이스에 넣어주는 함수를 create가 실행한다.

```
def create(req):

    # 객체하나 생성해서
    blog = Blog()
    
    # 받아온거 하나씩 받아오는 거임
    blog.title = req.GET['title']
    blog.body = req.GET['body']
    blog.pub_date = req.GET['date'] # timezone.datetime.now()
    print(blog)

    # 쭉 넣은 객체를 저장해라.
    blog.save()
    # 객체.delete() 는 삭제해라
    # url은 문자열이기때문에 str함수를 써주는 것이다.
    return redirect("/detail/"+str(blog.id))
```

#### render와 redirect의 차이는?

인자에 따라 달라진다.

redirect는 인자로 url을 입력할 수 있다.

`redirect(https://www.google.com)` 이런 식으로, 

프로젝트 외의 url에 연결을 할 수 있는 것이다.

render의 경우 파이썬으로 처리한 데이터를 페이지에 담아서 띄워주고 싶을 때 사용하는 것이다.

## 4.4_portfolio (static)

### 4.4.1_정적파일과 동적파일

#### 정적파일

미리 서버에 저장되어 있는 파일.

서버에 저장된 그대로를 서비스해주는 파일이다.

사용자가 요청보내면 준비된 내용을 그대로 보내주는 것

1. static: 개발할때 이미 준비해둔 파일
2. media: 웹 서비스 이용자들이 업로드 하는 파일

#### 동적파일

서버의 데이터들이 가공된 다음 서비스 되는 파일이다.

상황에 따라 (누가 어디서 언제 어떻게) 내용이 달라질 수 있다. 

`우리는 이번 시간에 정적파일을 다루는 법을 배울 것이다`

1. 미리 준비해둔 사진 띄우기
2. 사진 업로드 해보기

### 4.4.2_static 파일들의 처리과정

1. static 파일들의 위치찾기
   - static 파일들을 담을 폴더 만들기 - app 안에 static폴더 만들고 그 안에 파일 넣기 
   - static 파일이 어디있고, 어디로 모을지 알려주기 - setting.py에서 알려주기
2. static 파일들을 한 곳에 모으기 - pyrhon manage.py collectstatic

## 4.5_Media

업로드 된 이미지들이 들어올 디렉토리 경로와 url을 지정해줘야한다.

프로젝트가 미리 준비하지 못한 파일을 (사용자가 업로드 하는 파일) 저장했다가,

사용자에게 띄우는 것이다.

**즉,**

`static`은 외부와의 통신이 **없고**,

`media`는 외부와의 통신이 **있다**는 것이 차이점이 되겠다. 

장고는 **URL**을 통해 외부와 통신하므로, 

`media`는 디렉토리와 더불어 url설정을 해줘야 하는 것이다.

### 4.5.1_tip

사용자가 우리의 서비스를 이용할때  가장 먼저 반응 하는 것이 url이고,

url을 통해 들어온 정보가 mtv 패턴에 따라 처리 되는 것!

### 4.5.2_static ve media

static

1. static 파일이 어디있고
2. 어디로 모을지

media

1. media 파일이 어느 url을 타고
2. 어디로 모을 것인지

- settings.py에서 media설정(디렉토리와 url)
- url.py 설정
- models.py에서 업로드될 데이터 class정의
- DB에게 알려주기 위해 migrate
- admin.py에 모델 등록
- views.py에 모든 객체 내용을 보여달라는 함수 만들기
- html 띄우기

### 4.5.3_Media

#### settings.py

```python
MEDIA_ROOT = os.path.join(BASE_DIR,'media')
# 무슨무슨 홈페이지 / 미디어 / 파일 url 이렇게 설계하겠다는 것이다.
MEDIA_URL =  '/media/' 
```

#### urls.py

url은 settings에서 어떻게 설계할지 적어놨으므로, 

병렬적으로 추가해야 한다.

```python
from django.conf import from django.conf import settings
from django.conf.urls.static import static
```

## 4.6_템플릿 상속

코드의 재사용과 일관된 UI구성 및 변경이 용이하다.

1. 최상위 폴더에 templates 폴더를 만들고,
2. 모든 html의 뼈대가 되는 base.html을 만든다. 
3. 그리고 중복 코드 내용을 채워놓고,
4. settings.py 에 base.html의 위치를 알려준다.

```html
{% block content %}
넣어줄 콘텐츠
{% endblock%}
<!-- 상단의 메뉴바 같은 것은 base.html에 적어 두고 내용만 바꿔끼는 것이다.-->
```

상속받는 html 에서는

```html
{%extends 'base.html'%}
```

위와같은 코드를 상단 첫째줄에 입력하여주면 된다

## 4.7_URL을 효율적으로 관리해보자

앱이 많아지다보면 url이 많아지고, 한눈에 파악하기도 어려워진다. 

이러한 문제를 해결하기위해 앱별로 url을 만들어 관리해보자.

앱안에 urls.py를 만들면 된다. 간단하다!

url을 지정해 주는 방식은 똑같으며, project의 url에 include를 통해 붙여주면 된다.

```python	
from django.urls import path, include

# ... 생략

path('blog/', include('blogapp.urls'))
```

# 05_5주차

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

# 06_6주차

## 6.1 form 이론

forms.py 이라는 파이썬 파일을 하나 만들어 주고,

Model 형식에 맞는 입력 공간을 만들어보자.



HTML로 일일히 쳐줄 수 있지만,

1. 모델이 바뀌거나 추가가되면 그에 맞는 폼태그를 변경하거나 새로 만들어줘야하고,
2. 넘어온 데이터의 유효성 검사와 예외 처리가 쉽지 않다.
3. 폼 전체를 입력받고 싶을 때도 있고, 일부를 입력 받고 싶을 수도 있는데 이럴 때 응용하기 쉽지 않다.



따라서, 장고의 기능을 활용하여 좀 더 쉽게 해보자!

Form 만들기는 Model 만들기와 유사하니 그리 어렵지 않을 것이다.

### 6.1.2 Forms.py

`models.py -> DB`,

`form.py -> html의 <form>`

이렇게 맵핑 된다고 생각하자.

form 은 장고에서 기본적으로 제공하는 기능이며,

**모델을 기반으로 한 입력 공간을 만들 수도 있고**

> from django import forms.ModelForm

**아무 임의의 입력공간을 만들 수도 있다.**

> from django import forms.Form

### 6.1.3 모델 기반 입력공간

**forms.py **

```python
from django import forms

class myForm(forms.ModelForm):
    class Meta: # 클래스 안의 클래스
        # 어떤 모델을 기반으로 한 입력 공간인가?
        # 그 모델 중에서 어떤 항목을 입력 받을 것인가?
```

**views.py **

```python
from .form import myForm 

def create(request):
    수행 역할
    1. 처음 new.html에 들어갔을 때 빈공간 띄우기
    2. 이용자가 입력한 값을 처리하기

```

### 6.1.4 임의의 입력 공간

```python
from django import forms

class myForm(forms.Form):
    img = forms.ImageField
    text = forms.TextField(or forms.CharField)
    time = forms.DateTimeField
```

Models.py에 모델을 만들때와 유사하다는 것!

이처럼 forms.py를 통해 파이썬 파일을 분리하여 폼을 쉽게 관리하고, 폼을 생성할 수 있다.

## 6.2 TIP

**forms.py에서의 임의의 폼**

```python
max_num = forms.ChoiceField(choices = [('1','one'), ('2', 'two')])
```

위와같은 필드를 통해 선택 폼을 만들 수 있다.

`('값','선택항목(사용자들에게 보이는)')`

> HTML 보다 좀 더 논리정연하고, 관리하기 쉽다!

# 07_7주차

## 7.1 소셜 로그인 기능 구현

장고에서 소셜 로그인 기능을 지원하는 기능은 꽤 많다.

그중에 장고의 pip 패키지 중 하나인 **allauth**를 구현해 볼 것이다.

__차이?__

기존의 login 방식

- sqlite3라는 db에 저장이 됩니다.
- DB와 DB를 다루는 로직이 한 공간에 존재

소셜로그인 방식

- 로그인 함수를 실행시키면 구글서버나 카카오톡, 페이스북 서버에 들어가는 것이다.
- 해당 소셜의 서버에서 리퀘스트와 토큰 등을 주고 받으면서 로그인 실행.

__setting.py에서 해주어야하는 것들__

1. INSTALLED_APPS

```python
	...
    
    'django.contrib.sites',

    # allauth

    'allauth',
    'allauth.account',
    'allauth.socialaccount',

    # provider 구글 페이스북 카톡 깃헙
    # 소셜로그인 기능을 제공해주는 업체. 

    'allauth.socialaccount.providers.google',
    
    ...
```

2. 보기편한 곳에 새로운 튜플 추가

```python
AUTHENTICATION_BACKENDS = (
    'django.contrib.auth.backends.ModelBackend',
    'allauth.account.auth_backends.AuthenticationBackend',
)

SITE_ID = 1

LOGIN_REDIRECT_URL = '/'
```

__urls.py__

```python
 # 이미 url은 allauth를 설치할때 설정된 것이다. 
    # 따라서 우리는 가져오기만 하면 된다.
    path('account/', include('allauth.urls')),
```

__그 후?__

내가 제공하고자 하는 프로바이더와 (구글) Social accounts를 연결해주어야한다.

admin으로 들어가서 `Social application` 모델에 들어가 연결해주자 

> Client id 와 Secret Key는 구글에 들어가서 받아오도록 하자.

> 구글 api에서 프로젝트를 만들어서 받아오면 된다.

## 7.2 API

Application Programming Interface

우리가 만든 웹서비스에서 사용할 수 있도록, 

우리가 갖고 있지 않은, 사용하고 싶은 외부기능들을

제어할 수 있는 연결통로(연결 수단)를 뜻한다.

# 08_8주차

## app 재사용 이론

하나의 기능과 역할만을 담당하도록 설계된 것이 App이다.

다른 웹사이트를 개발하다보면, 공통적인 기능을 가지는 app이 존재할 것이다.

이를 **패키징**하여  다른 프로젝트에서도 사용하도록 해보자.

재사용하고자 하는 앱을 패키징하여, 다른 프로젝트에서 이를 설치하는 과정으로 이루어진다. 

__패키징 시 필요한 것__

1. 패키지의 소개 (사용설명서, 기능명세서) `readme.rst`
2. 라이센스 `LICENSE`
3. 설치의 방법 과정 `setup.py`
4. 파이썬 파일이 아닌 파일들 명시 `MAINFEST.in`

## PostgreSQL 연동, 이론

서비스가 커질 수록, 장고에 내장되어있는 sqlite로는 감당하기 힘들어 질수있다.

이런 상황일 경우 다른 DB와 연동하는 것이 필수적인데, 많은 DB중 PostgreSQL를 이용하보도록하자.

무료이며, 설치가 쉽기 때문이다.

> 점유율이 높은 MySQL도 추천한다!

기본적으로 장고는 sqlite를 디폴트 DB로 여기고 있으며, `settings.py`에 설정되어있다.

DB를 변경하고자 할 때는, `settings.py`의 `DATABASES` 항목을 변경해주면된다.

### 다른 DB연결하기

1. 다른 DB 설치
2. DB 연결 (가리키기)
3. migrate를 통한 연결

## AWS 배포

# 부록

## Model?

데이터의 구조나 형식이다.

우리는 데이터를 정의하고 싶을 model 안에 정의를 해왔다.

```python
class 데이터이름:
    데이터형식 (사진, 글 등등)
    데이터형식
```

내가 표현하고자 하는 어떤 형식의 데이터, 

데이터 베이스에 넣고자 하는 데이터를 클래스(객체)로써 나타내는 것을

**ORM(Object Relational Mapping**이라고한다.

즉, 객체로 관계형 DB를 다룰 수 있게끔 해주는 것이다.

따라서 장고는 ORM방식으로 DB를 다루기 때문에,

 특별한 SQL문 없이도 DB안에 적용할 수가 있는 것이다.

> DB에게 알아듣게 하는 과정이 `python manage.py makemigrations/migrate` 인 것이다

## ORM & CRUD

ORM 방식을 이용하여 데이터를 넣어주었다고 하자.

그 후 우리는 데이터를 어떻게 다룰까?

==> **추가 열람 수정 삭제**

> Create Read Update Delete

백엔드에서 가장 중요한 본질이다.

정보를 조회하고 수정하고 생성하고 삭제하는 것.

아주 기본적이며 꼭 필요한 기능들이다!

## CBV

## class based view (Generic view)

함수와 클래스는 callable object 라는 공통점을 갖는다.

django의 view는 callable object로 정의하기에 클래스로도 가능하다.

__이제와서 굳이 클래스를 사용하는 이유?__

클래스에는 있는 결정적인 장점, 바로 `상속`이다.

중복의 제거와 코드의 상속을 통해 코드의 수를 줄이고 유지보수를 편하게 만들어보자는 것.

__규칙을 지켜주어야 하는 html__

list를 보여줄 때 는 object_list에 모든 객체가 담겨서 온다.

detail 페이지로 넘어갈 때는 그 특정 객체가 object에 담겨  들어간다.



