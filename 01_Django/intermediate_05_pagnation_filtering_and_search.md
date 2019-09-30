## Pagination

우리는 API서버를 만드는 것인데 왜 페이지네이션이 필요할까? 하나의 요청만으로 처리하기 어려운 레코드들을 여러 요청으로 나누어 전송하기 위함이다!    

페이지 네이션을 적용할 때에는 반드시 레코드를 정렬한 상태에서 수행하도록 하자.

> 특정 쿼리셋에만 정렬을 적용하고 페이지네이션 하고 싶다면 order_by('id') 를 써서 정렬해도 좋다. 모든 모델에 대해 정렬하고 싶으면 메타 클래스에서 order를 미리 넣어주자.

### 어떻게 구현하나?

매우 간단하다. settings.py만 추가해주면 된다.

```python
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.LimitOffsetPagination',
    'PAGE_SIZE': 100
}
```

### 특정 모델만 다른 페이지 단위를 다르게 하고 싶은 경우

```python
from rest_framework.pagination import PageNumberPagination

class Mypagination(PageNumberPagination):
    page_size = 5

class PostViewSet(viewsets.ModelViewSet):
    ...
    pagination_class = MyPagination
```



## filtering and search

### filtering

request를 걸러보낸다.  예를 들어 내 글보기 같은 경우 user1 이라는 user로 작성된 글들을 보여줘! 라고 하는 경우 이에 맞게 걸러진다.

### search

response를 걸러받는다. 내가 받은 reponse가 있는 상태에서 특정 모델의 특정 컬럼을 대상으로 문자열을 찾고자 하는 것이다. 

> 포스트 모델의 title을 대상으로 '졸려' 라는 문자열이 포함된 글들의 목록만 보여줘.

