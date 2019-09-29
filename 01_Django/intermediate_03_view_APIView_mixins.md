## View of DRF

__ViewSet__

CRUD(View)를 설계하는 쉽고 간단한 방법

__배울 순서__

장고 기반의 cbv와 비슷한 rest framework의 APIView를 통해 view 설계를 해보고, mixins, Generic CBV, ViewSet의 순서로 배워보자!



## API View

APIView를 상속하여 View를 설계할 땐 status와 Response를 import 해와서 직접 응답과정을 만든다.

> import한 status를 바탕으로 직접 response를 만들어 보내는 것이다.



__detail class__

원하는 기능의 cbv를 사용할 때는 내가 필요로 하는 http method의 이름으로 메소드 이름을 정의하면 된다. 아래의 코드를 보자.

```python
class SnippetDetail(APIView):
    """
    Retrieve, update or delete a snippet instance.
    출처 django rest framework 홈페이지
    """
    def get_object(self, pk):
        try:
            return Snippet.objects.get(pk=pk)
        except Snippet.DoesNotExist:
            raise Http404

    def get(self, request, pk, format=None):
        snippet = self.get_object(pk)
        serializer = SnippetSerializer(snippet)
        return Response(serializer.data)

    def put(self, request, pk, format=None):
        snippet = self.get_object(pk)
        serializer = SnippetSerializer(snippet, data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def delete(self, request, pk, format=None):
        snippet = self.get_object(pk)
        snippet.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

디테일에서 사용하는 기능은 get, put, delete 이기 때문에, 이름을 이와 같이 정한 것이다.

```python
class anything(APIView):
	def 필요로하는 http method:
		원하는 http method로 어떻게 처리할지 직접정의
        (내부에 어떻게 동작할 것 인지)
```

위와같이 내 의도대로 함수를 정의할 수 있다는 것이 장점이다!