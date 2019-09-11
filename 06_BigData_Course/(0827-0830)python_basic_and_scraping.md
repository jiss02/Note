## python 기초 

__dict.get 함수__

```
dict.get('key', '키가 없을 때 리턴할 값')
```

__dctionary__

키값 중심의 자료 컨테이너.



## 데이터의 정규화

### min - max 알고리즘 (Normalization)

열의 `min = 0` 으로, `max = 1` 로 맞추는 것

`new_X = (old_X - min) / (max - min)`

### 표준화 (Standardization)

열의 `mean = 0`으로, `std = 1`로 맞추는 것

`new_X = old_x - mean(열) / std(열)`

조금 더 성능이 잘 나와 주는 것은 표준화이다!

> 협의의  Normalization은 위의 min-max algo 이고, 광의의 경우 위의 두개를 전부 포함한다.



## 구글 API 사용법 찾는법

`라이브러리 검색 -> documentation -> clients library (or get start) `

새로운 라이브러리를 접할 때 이를 참고하여 사용법을 익히도록하자.



## Server

1. DataBase
2. Back end
   - JAVA, PHP, RUBY, DJANGO, JS
3. Front end
   - 사용자에게 보여지는 부분
   - HTML, CSS, Js

이 세개를 가능하게 하는 것들이 모여있는 컴퓨터가 서버라고 보면 된다.



## url

`https://search.naver.com/search.naver?sm=tab_opt&where=nexearch&query=미세먼지&oquery=al세먼지&tqi=UTNXilprvxZssRL5wJNssssstaG-043644&nso=so%3Add%2Cp%3A1y%2Ca%3Aall`

- 파이썬 함수에 쿼리들이 들어간다.
- `?` 뒤는 커리문으로, 서버로 데이터를 보낸다.
- `&` 는 다른 쿼리문이라는 것을 알려주는 구분자이다.
