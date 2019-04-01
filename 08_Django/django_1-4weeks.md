# 1주차

## 기본환경 셋팅

프로젝트를 위해 장고를 설치할 때에는, 가상환경을 만들어 설치하자.

하나의 통안에 담는다고 생각하는 것이 좋다! 다른 프로젝트에는 영향을 미치지 않도록 하기 위함이다. 

> 여러 프로젝트를 수행하며 프로그램들이 꼬일 수 있거나 무엇을 설치했는지 헷갈릴 수 있기때문이다.

1. `python -m venv <name>`
2. `source <name>/Scripts/activate`
3. `deactivate` (가상환경 종료)
4. `pip install django`

## hello world 이론

Django는 어떤 과정을 거치며 데이터가 처리될까?

- 데이터가 여러 파일들 사이에 티키타카로 전송된다.

### 어디서 티키타카를 하는가?

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

### 어떻게 티키타카를 하는가?

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

## hello world 실습

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

