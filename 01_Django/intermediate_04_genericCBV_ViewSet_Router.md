## Generic CBV

mixins에서 중복되는 코드마저 제거하기 위해 등장했다! 크게 어려운 것이 없으니 [rest framework 공식문서](https://www.django-rest-framework.org/tutorial/3-class-based-views/)를 참고하자.



## ViewSet

ViewSet은 크게 구현되있는 것이 없다. 인자로 상속받은 두개를 엮어주는 과정에 불과하기 때문이다. ReadOnlyModelViewSet 클래스와 ModelViewSet 클래스를 중점으로 보도록 하자.

### ReadOnlyModelViewSet

```python
class ReadOnlyModelViewSet(mixins.RetrieveModelMixin,
                          mixins.ListModelMixin,
                          GenericViewSet):
    pass
```

상속받는 3개의 클래스를 묶어주는 역할을 한다. 엄밀히 말하면 객체나 레코드들의 목록을 가져다주는 list()와 특정 객체를 갖다주는 역할인 retrieve() 메소드를 묶어주는 것이다! 

> 즉, 레코드들을 읽을 수 있게 도와주는 읽기 기능 ViewSet 인 것이다!

ROMV는 하나의 VeiwSet으로 List와 Detail을 구현가능하게 해준다.

__views.py에서의 사용__

```python
class PostViewSet(viewsets.ReadOnlyModelViewSet):
    queryset = Post.objects.all()
    serializer_class = PostSerailzer
```

### ModelViewSet

List와 Detail뿐만 아니라 커스텀 api요청까지 처리하는 것 까지 가능하다!

```python
from rest_framework.decorators import action
from rest_framework.response import Response

class SnippetViewSet(viewsets.ModelViewSet):
    """
    This viewset automatically provides `list`, `create`, `retrieve`,
    `update` and `destroy` actions.

    Additionally we also provide an extra `highlight` action.
    """
    queryset = Snippet.objects.all()
    serializer_class = SnippetSerializer
    # 액션을 수행할 수 있는 권한을 설정하는 부분
    permission_classes = [permissions.IsAuthenticatedOrReadOnly,
                          IsOwnerOrReadOnly]

    # @ + 함수들 ==> decorator, 장식자	
    # custom api를 위해 쓰인다!
    @action(detail=True, renderer_classes=[renderers.StaticHTMLRenderer])
    def highlight(self, request, *args, **kwargs):
        snippet = self.get_object()
        return Response(snippet.highlighted)

    def perform_create(self, serializer):
        serializer.save(owner=self.request.user)
```

단 두줄로 crud를 구현할 수 있는건 좋지만 다른 logic은 어떻게 구현하면 좋을까? 이럴 땐 `@action`을 사용하여 custom api를 만들 수 있다!



## Router

ListView와 DetailView의 처리를 위해 필연적으로 두개의 path함수가 생긴다.  이 여러 path를 묶어줄 방법이 필요하다.

`path함수를 묶어준다 == path함수의 두번째 인자를 묶는다`

그렇다면 실제로 어떻게 함수들을 묶을까?

### .as_view()

as_view는 사실 괄호안에 딕셔너리 형태의 인자를 받는다.

`as_view({'http_method':'처리할 함수'})`의 형태로 넘겨준다면 함수를 묶을 수 있게 된다!

자세한 코드는 rest_framework 공식문서의 router항목을 참조하자.

### DefaultRouter

관례적인 매핑관계를 가지고 있는 클래스이다. 