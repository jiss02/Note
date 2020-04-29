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

> (이클래스안에서 가져올건데, 몇번째 값을 가져와줘)



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

# 