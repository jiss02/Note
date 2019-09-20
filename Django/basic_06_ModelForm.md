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