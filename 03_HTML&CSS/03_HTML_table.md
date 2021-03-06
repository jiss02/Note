# HTML

## 테이블과 리스트

## 테이블

표형식을 이용하면 깨끗하게 데이터를 정리해서 쓸 수 있다.

표를 만들기 위해서는 `table`태그를 사용하면 되며,

정해진 형식과 태그들이 존재한다. 

### table 태그

- 표전체를 담는 `table` 태그
- 각 행을 담는 `tr` 태그
  - table row
  - tr 태그를 기준으로 데이터를 넣어야한다. 
- 데이터하나하나를 담는 `td` 태그
  - table data
- 컬럼을 담는 `th` 태그
  - table heading

__순서__

1. 테이블을 만들고
2. 행의 개수만큼 행을 만들고
3. 컬럼을 넣고
4. 데이터를 넣자

__왼쪽에 컬럼을 넣고 싶다면?__

tr 태그를 기준으로 잘 넣자.

__칸을 합치고 싶다면?__

`rowspan="숫자", colspan="숫자"`를 써주자.

적혀진 숫자만큼 각각의 행과 열을 점유한다. 

## 목록

### ul

unordered list: 순서가 없다.

### ol

ordered list: 순서가 있다.

```html
<ol>
    <li>요소1</li>
</ol>
```

목록은 기본적인 들여쓰기가 되있으며, 리스트의 중첩도 가능하다.

### 목록과 관련있는 속성

#### ol 태그

- start = "숫자"
  - 리스트의 시작하는 숫자를 정한다.
- type = "문자"
  - 순서를 시작하는 문자를 정한다.
- reversed
  - 순서를 반대로 한다.

### li 태그

- value = "숫자"
  - 해당하는 리스트에게 번호지정. 
  - 그 뒤의 리스트는 그 value를 기준으로 숫자가 매겨진다.
