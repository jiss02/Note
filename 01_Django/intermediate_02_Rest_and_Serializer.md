## Rest

### REST Architecture는 무엇인가 

`REpresentataional State Transfer` 의 약자이며, HTTP를 이용해 통신하는 네트워크상에서 규정된 약속이다. 인터넷에서 얻을 수 있는 모든 데이터를 퉁쳐서 자원이라고 하며, 자원을 대표하는 단어 or 식별자로 자원의 상태를 전송하겠다는 뜻이 된다.

즉, 자원을 이름으로 구분하여 상태를 전송하겠다는 것이다.

### 왜필요한가?

독립적인 운영과 발전의 측면에서 필요하다. 기존의 약속을 깨뜨리지 않고 독립적으로 발전할 수 있는 것이다. 일일히 패치 사실을 알리지 않아도 되도록 하여 독자적으로 발전하도록 하여 네트워크 생태계의 발전을 돕는 것이다.

### REST의 설계조건

REST의 원칙대로 지키고 설계하면, 기존의 룰을 깨트리지 않으면서 네트워크의 독립적 발전을 돕는 REST가 되는 것이다. 그 조건은 다음과 같다!

- Server - Client의 존재 필요
- STATELESS : 클라이언트의 이전상태를 기록하지 않는다. (http가 대표적임)
- Cache
- Uniform Interface
- Layered System
- Code-on-demand

### API 는 무엇인가

클라이언트가 손님이고 서버가 요리사라면, API는 클라이언트와 서버사이의 메신저인 웨이터라고 보면 이해가 쉬울 것이다. req와 res를 주고 받을 때 특정 형식에 맞추어 전달해 주는 것이다. 이 특정 형식을 설명해주는 것이 API문서이다. 

### REST API는 무엇인가

REST 아키텍쳐 스타일을 따르는 API인 것이다. 위의 REST 설계 조건을 따르면 된다!

> 이를 Restful 하다고 한다.

이해가 어렵다면 간단하게 HTTP(POST, GET은 method)로 CRUD를 구현할 수 있는 API라고 생각해두자.

### 현대의 REST API들은 잘 지키고 있을까?

현대의 REST API들은 사실 위의 조건들을 잘 지키지 못하고 있다. 데이터의 형식이 JSON이기 때문이다. JSON은 사용자가 정의하기 나름이기에 제 각각으로 데이터가 구성되며, 어떤 링크를 타고왔고 다음 링크가 어디인지 모르기 때문에 REST의 초기의도와 다르게 흘러갈 가능성이 높다. 독립적으로 발전해야 할 수 있어야 하지만 단순한 정보 만으로는 파악이 어렵기 때문에 이전 링크와 다음 링크를 통해 파악해야하기 때문이다.



## Serializer

ModelForm과 작동방식이 유사하다. 

- model로 부터 field를 읽어온다
- 유효성 검사가 가능하다.
- JSON 문자열로 전송한다.

### 기존 장고와 REST framework API의 유사도 비교

__기존 장고__

- html, css, js로 주고 받는다.
- POST 요청시 form에 담겨 처리가 된다.
- 유효성 검사가 실행된다.

__REST API__

- JSON문자열을 통해 데이터를 주고받는다.
- POST요청시 JSON을 문자열화 시켜 처리가 된다.
- 유효성 검사가 실행된다.

둘의 방식은 매우 비슷하다는 것을 알 수 있다.

### rest_framework

기본 코드를 완성하고 runserver를 실행하면, DefaultRouter에 의해 API의 가장 기본이 되는 서버페이지로 이동된다.

`GET (url) `: 이 url로 요청하면 원하는 메소드를 실행할 수 있다는 것이다.

__POST__

API 서버 페이지에 글을 작성하는 것은 POST요청과 같다. JSON방식으로 전송된다.

__OPTIONS__

객체에 대한 자세한 내용을 나타내는 페이지

> id값은 사람들이 마음대로 수정하면 안되므로 read_only가 설정이 되어있다.

__read_only 설정__

serializer.py 의 class Meta 밑에 작성해주면된다.

`read_only_fields = ('title',)`

> 읽기전용으로 하고싶은 column 명 추가

### Serializer 실습

크게 다른 것만 살펴보자.

### urls.py

```python
from django.contrib import admin
from django.urls import path, include
from . import views
from rest_framework.routers import DefaultRouter

# restful framework는 라우터를 통해 url을 결정하는 구나.

router = DefaultRouter()
# 모델 소문자
router.register('post', views.PostViewSet)

urlpatterns = [
    path('', include(router.urls))
]
```

### serializer.py

```python
from .models import Post
from rest_framework import serializers

# API상의 crud담당

class PostSerializer(serializers.ModelSerializer):
    class Meta:
        model = Post
        fields = '__all__'
        # fields = ['title', 'body']
        read_only_fields = ('title',)
```

### views.py

```python
from django.shortcuts import render
from .models import Post
from .serializer import PostSerializer
from rest_framework import viewsets

# Create your views here.
# 시리얼라이즈는 cbv임.

class PostViewSet(viewsets.ModelViewSet):
    queryset = Post.objects.all()
    serializer_class = PostSerializer
```

