# CSS

css의 기초를 배우고, 개념을 정리하는 공간입니다.

어떠한 개념을 잠시 까먹었을 때, 빠르게 검색하고 복습하기위해 필기합니다.

### 01

생활코딩 web2 css 강의를 들으며 필기한 공간입니다.

### 02

멋쟁이 사자처럼의 css 기초 수업을 들으며 필기한 공간입니다.

# 01_생활코딩 CSS

## css

HTML과는 다른 컴퓨터 언어이다. 디자인에 대한 근본적인 해결책이 필요하다 느껴 등장하게 된 새로운 언어.

- a 태그나 h1 태그는 정보를 주는 중요한 태그이다.
	- font와 같은 태그를 쓸수 있지만, 정보로써의 가치가 하락한다.
- 디자인 자체는 정보가 아니다.	

## css - 등장배경과 기초지식

웹 브라우저는 기본적으로 HTML이라고 생각하므로 css문법에 맞게 처리하도록 해야한다.

### css 를 표현하는 방법

#### style 태그

__style__ 태그를 사용하여 그 안에 css를 사용한다.

- head 태그 안에 들어간다.
- style은 html 문법이면서, 태그 안에 있는 것은 css 문법에 따라 처리하도록 하는 것이다.
> 주석 처리: <!--

- font 태그는 html사용, style 태그 안에 작성한 것은 css. 훨씬 간편하다. 
- 중복의 제거가 중요하다! css를 통해 중복을 제거할수 있게 된 것.
> 중복이 있는 모든 코드를 바꿀 때, 의도되지 않은 것까지 바꿀 수도 있다는 위험이 있음.

- 유지보수를 편리하게 할 수 있고, 가독성도 높아진다.
- 디자인과 관련된 코드는 style 태그에 갇힌다. 
	- 디자인 부분은 거르고, 정보가 있는 필요한 부분만 긁어서 사용할 수 있다.
	- 정보 전달에 전념하기 위해서 HTML에서 디자인을 빼온 것이 css. 훨씬 효율적이다.

#### style 속성

효과를 특정 값에게 적용하기 위해서 사용하는 속성. 해당 속성은 html의 속성이며, 그 값으로 반드시 css의 효과가 들어온다.

- a{}: 선택자; 효과를 누구에게 줄것인가를 선택하므로!
- color:black == 선택자에게 지정될 효과, 선언
> 선택 된 태그에게 효과를 주는 것

## 기본문법

- 여러개의 효과를 지정할 때, 세미콜론으로 구분.

```
     a { # Selector
       color:black; #Property:Value
       # declaration
    } 
```

- 디자인을 위해 어떤 property가 존재하는가?
- 효과를 정확하게 선택하여 지정하기 위해 다양한 선택자를 알자. 

### 효과와 선택자

- 검색엔진을 통해 필요한 property를 찾는 것이 중요하다.

### class 속성

HTML의 문법으로 클래스를 지정해준다. style 태그 내에서 사용할때는 __.name__의 형식으로 입력해주어 class이름이 name인 것들을 적용하도록 한다.

- class 속성의 값은 여러개의 값이 들어올 수 있으며, 띄어쓰기로 구분한다.
- 하나의 태그에는 여러개의 속성이 들어갈수 있고, 여러개의 선택자를 통해 하나의 태그를 공동으로 제어할 수 있다.
- 보다 가까이에 있는 명령이 더 큰 영향력을 갖는다. 

#### id 선택자

- 선택자 앞에 #을 붙이면 된다.
- id 선택자가 class 선택자보다 우선한다.
- 클래스 선택자는 태크 선택자보다 우선한다.
- 즉, __id > class > tag__
- id의 값은 단 한번만 등장해야한다. 중복 X.
- 구체적인 것이 포괄적인 것보다 우선한다. 
> 태그를 뒤에 쫙 깔고 특정한 것 몇개를 id로 딱딱 바꿔주기

- 선택자들의 조합에 따라 효과를 원하는 대로 넣어줄 수 있다.

## 박스모델

__태그 마다__ 성격과 일반적인 쓰임에 따라 화면 전체를 쓰는 것이 편한 것과, 자신이 쓰는 것만큼의 부피를 갖는 것이 편한 것으로 나뉜다.  

- 화면 전체 사용: __block__ level element
- 자기 자신의 부피만큼 : __inline__ element
	- 넓이나 간격 등 변경 가능하다.
	- vhr width 높이 height

- border-something 의 형태.
- border:5px solid red; 의 형태로 압축도 가능.
- padding property: 테투리와 content사이의 간격
- margin: 테두리와 테두리사이의 간격
- shift+ctrl+c 를 통해 태그가 어떤 css의 영향을 받는지 쉽게 파악이 가능하다.
- html 태그 하나하나를 박스 취급하고, 부피감을 결정한다.

## 그리드

- div: 디자인을 위한 아무런 의미가 없는 태그 
	- block level element	
- span: div와 같은 용도
	- inline element
- 1fr
	- 자동으로 화면 전체 중 일정 비율을 쓰도록 해놓는 것
- display 속성
	- none : 보이지 않음
	- block : 블록 박스
	- inline : 인라인 박스
	- inline-block : block과 inline의 중간 형태
- 복수의 태그를 하나의 그룹으로 묶어 그리드로 포함되는 요소로 사용하려면 그것을 감싸는 공통의 부모 태그가 필요하다.
- 부모가 있는 경우 #grid ol과 같은 식으로 사용하면 된다. 나중에 ol태그가 겹칠 수 있기 때문에!

## 반응형 웹, 반응형 디자인

- 화면의 크기에 따라 웹페이지의 요소들이 반응하여 적절한 형태를 갖추는 것. 
	- 다양한 환경에서 적응가능
- media quary를 사용하자.

## CSS 코드의 재사용

- link 태그를 통해 css파일을 연결할 수 있다.
- 재사용성도 높아지고, 효과적인 변경이 가능해진다.
	- 다운받는 코드의 양도 줄어든다! 
	- 유지보수가 편리해지는 것이다.
- 네트워크의 트래픽을 적게 사용하면서도, 빠르게 웹페이지를 보여줄 수 있게 된다. 

# 02_멋쟁이 사자처럼 CSS

## 선택자와 속성

## 값과 단위

프로퍼티가 다양한 만큼, 다양한 값이 존재한다.

하지만 프로퍼티별로 사용할 수 있는 값은 정해져 있으니 잘 파악하도록 하자.

### 들어갈 수 있는 값의 종류

1. 숫자값: 글자크기, 너비, 높이 등..
   - px
     - 절대 길이이다.
     - 픽셀을 의미한다. 
     - 디스플레이를 구성하는 최소 단위이다.
   - em
     - 상대적인 길이를가진다.
     - 현재 스타일이 지정된 요소의 font-size 기준.
   - rem
     - 상대 길이를 가진다.
     - 최상위 요소의 font-size 기준.
     - 최상위 요소는 html 태그를 의미한다.
     - 상속이나 반응형 웹사이트와 같은 것을 대비하기 위해 rem을 쓰는 것이 권장된다.
   - %
     - 상대 길이이다.
     - 이미지나 레이아웃의 너비나 높이를 지정할 때 쓴다.
2. 색
   - blue나 orange같은 키워드는 편리하지만 다양한 색을 나타내는 것에 한계가 있다.
   - hex code: #000000의 형태로 쓰여진다.
   - rgb: red, green, blue의 수치를 지정해주어 색을 나타낸다. 

## 텍스트와 관련된 프로퍼티

font-size, font-family, font-style, font-weight가 대표적이다.

### 텍스트 스타일과 크기에 관련된 속성

#### font-family

글꼴을 설정하는것으로, 

내가 설정한 폰트가 사용자에게 없을 수도 있으므로 여러개를 지정해 주는 것이 좋다.

##### 웹폰트

local에 없더라도 손쉽게 불러와서 사용이 가능하다.

> 구글 웹폰트를 방문해보자!

#### font-stlye

**bold**와 *italic*을 설정할 수 있다.

oblique는 italic이 없더라도 무조건 글자를 기울여서 쓸 수 있다.

#### font-weight

굵기를 100 ~ 900 으로 표현할 수 있게해주는 프로퍼티이다.

400은 normal, 700은 bold의 크기이다.

### 텍스트 정렬과 관련된 속성

#### text-align

텍스트를 좌, 우, 중앙 정렬.

left, center, right가 가능하다. 

본인(자기자신) 요소를 기준으로 정렬을 한다.

#### line-height

문장사이의 간격 조정.

그냥 숫자만 넣으면 해당 요소의 폰트 사이즈의 배수로 계산하여 넣어준다.

#### letter-spacing

자간을 의미

#### text-indent

문단의 시작부에 들여쓰기를 함

## 박스모델

html의 모든 요소는 상자 형태를 가진다.

contents를 감싸는 전체를 뜻하며, 

content, margin, border, padding으로 이루어져 있다.

## 위치와 관련된 프로퍼티

### display 프로퍼티

요소가 보여지는 방식을 지정한다. 요소들은 전부 해당 속성을 기본적으로 가지고 있다.

1. block
   - width 100%를 기본으로 가진다.
2. inline
   - 요소의 contents만큼만 width를 가진다.
   - width, height, margin-top과 bottom 불가능.
3. inline-block
   - inline의 한계를 보완하는 값
   - inline요소와 block요소의 특성을 모두 가진다.
   - inline에서 불가능 했던것이 전부 설정 가능 해짐.
4. none
   - 숨겨지고 출력이 되지 않는다.

### position 프로퍼티

요소의 위치를 정의한다. 

1. static
   - 기본값이며, 좌표 설정이 불가능하다.
2. relative
   - 상대위치이며, 기본위치(원래 있어야할 위치)를 기준으로 좌표를 사용한다.
3. absolute
   - 절대위치.
   - 부모나 조상중 static을 제외하고 선언된 곳을 기준으로 좌표 프로퍼티 적용.
4. fixed
   - 특정 좌표에 고정시키는 것.
   - 스크롤을해도 고정되어있는 것이다.