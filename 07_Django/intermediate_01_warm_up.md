## JSON

자바스크립트 객체로서 수행할 수 있도록 하는 가벼운 문자열 데이터 표현식. 가벼운 상자정도로 보면된다.



## REST

기존의 서버에서는 HTML과 CSS, 그리고 JS를 주고 받는다. 하지만 REST에서는 딱 데이터만 주고 받는다. 스타일이나 로직 없이 요청과 응답만 담은 의사를 전달한다.

기초 과정은 요청을 보내고 html을 렌더링했다면, 중급에서는 REST라는 API 서버를 만들어 두고 JSON에 다가 요청에 따른 응답을 만들어 담고 보내주는 과정에 집중해야한다.



## 직렬화

JSON으로 표현된 것은 컴퓨터에게 애매하다. 이게 JS 객체인지 아닌지를 어떻게 구분한단말인가! 이런 고민을 해결하기위해 표현하고자 하는 데이터를 만국 공통 자료형인 `문자열`로 바꾸어 보내게된다. 이가 바로 **직렬화**이다.

> 네트워크 구성상의 메모리 문제도 있다.

사용자는 객체를 문자열로 바꾸어 서버로 보내고, 서버는 문자열을 객체로 바꾸어 사용자에게 보내게 된다.

```python
"""diary == 딕셔너리 데이터"""
dict_s = json.dumps(diary)
print(type(dict_s))

## ==> str
```



## CBV

클래스를 기반으로 한 뷰를 의미한다. 클래스를 통해 상속을 용이하게하고 코드의 중복을 줄여보자.

> 호출이 가능한 객체: 함수, 클래스

**왜 redirect가 아닌 reverse_lazy 인가?**

장고에서 제공하는 함수기반을 상속받아 사용하는 것이므로 이를 준수해주어야한다.

리버스 레이지는 리다이렉트와 같은 역할을 하며, 리다이렉트는 return 을 해주어야하지만, 함수형의 경우 리버스 레이지를 사용하여 success_url 변수에 무조건 담아주어야하는 것이다.

**Create시 다른 작업을 하고싶다면?**

상속이므로 클래스 밑에 함수를 쭉쭉 정의해주면 된다.
