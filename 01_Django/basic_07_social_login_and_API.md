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