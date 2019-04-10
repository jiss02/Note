# HTML

## FORM

**폼에 포함되는 다양한 입력 양식 태그들을 감싸준다.**

사용자로부터 데이터를 서버로 받을 때 다양한 입력 양식이 있는데,

이러한 양식들을 form태그들을 통해 만들 수 있다.

form태그는 하나의 신청서라고 보면 될 것이다. 

여기서부터 여기까지 폼입니다. 라고 알려주는 것이다.

### form태그의 속성

- action: 데이터를 보낼 url을 지정
  - 해당 데이터를 처리할 웹서버 url을 담고 있는 것이다.
- method: 보내는 방식을 지정
  - 데이터를 보내는 조금 특별한 메세지: `HTTP request Message`
    - 해당 메세지의 헤더에 목적지가 되는 서버의 url을 담는다.
  - get 방식
    - 폼에 입력한 데이터를 url뒤에 붙여 눈에 보이게 보낸다.
    - 데이터를 요청하고 받아 올 때 주로 쓴다.
    - 데이터 조회가 목적이다.
    - 주로 검색과 같은 경우에서 사용하며, 다른사람에게 url을 전달하거나 즐겨찾기를 할 때 용이하다.
  - post 방식
    - 보이지 않도록 메세지의 body부분에 숨겨서 적어 보낸다. 
    - 게시하다. 서버에있는 데이터를 쓰거나 수정할 때 사용한다.
    - url에 노출하게 되면 주소만으로도 삭제를 해버리거나 정보가 유출 될 수 있다.

> 전송방식의 차이이다.

```html
<!DOCTYPE html>
<html>
    <head>
        <title>클래스 라이언 실습 환경</title>
    </head>

    <body>
        <h2>회원가입</h2>
        <form>
            <input type="text" name="id" placeholder="이름을 넣으세요" value="hyun"><br>
            <input type="password" name="password" placeholder="비밀번호를 입력하세요"><br>
            <input type="text" name="id" placeholder="아이디를 입력하세요"><br>
        </form>
    </body>  
</html>
```

## input 태그

사용자에게 입력을 받기위해 사용되는 태그이며 빈태그이다.



### input 태그의 속성

- type=""

  - 인풋태그의 종류를 결정
- name=""

  - 같은 타입과 구분되는 이름을 결정
  - 서버로 데이터를 전송할때 입력받은 데이터를 구분하기 위해 이름을 지어주는 것이다.
  - name이 `key`가 되고 사용자가 입력한 데이터가 `value`가 된다.
- placeholder=""

  - input 칸 안에 아무 값도 입력 되지 않았을 때 나타나는 텍스트.
  - 실제 값이 아닌 하나의 가이드 문구라고 보면 좋다.
- value=""
  - 위의 플레이스 홀더와 약간다르다.
  - 실제 할당 되는 값으로, 초기값을 넣어준다고 보면 된다. 

## label 태그

각각의 input에 라벨을 붙여주는 역할이다.

`for`속성을 통해 라벨을 붙이고자 하는 input과 연결할 수 있다.

`<input id = "password">`와 `<label for = "password">비밀번호: </label>` 처럼 연결해 주면 된다. 

input 태그의 id와 label 태그의 for의 값을 일치시켜 연결시키는 것이다.

## select 태그

`name` 이란 **속성**을 반드시 가져야 하고, 

**option 태그**는 `value` 속성을 무조건 가져야한다. 

셀렉트의 네임과 옵션의 밸류가 짝을 이룬다.

```html
<select name = "gender">
    <option value="male">남성</option>
</select>

url에는 ~~~~/?gender=male의 형태로 들어간다.
```

## textarea 태그

한번에 많은 데이터를 받기위해 사용한다.

빈요소가 아니기 때문에 종료 태그가 필요하다.

## button 태그

input 태그에서도 버튼으로 제출이 가능하기는 하다. 

그러나 button 태그는 html요소를 안에 담을 수 있기에 유용하니 배워두자.

`<button type="submit">제출</button>`