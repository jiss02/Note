# FRI
***

## 코드

+ rm : 변수 지우기
+ tilble 이라는 자료구조는 창에 맞게 출력해주는 등의 기능이 들어가 있다.
+ nrow : 행의 개수 출력
+ dim(df)[1] : 첫번째 요소 
+ ctrl + shift + c : 주석입력

### 데이터 합치기

+ left_join(df1, df2(붙일거), by = "붙일기준") : 가로로 합치기.
> 키가 있어야 한다.

+ bind_rows(a,b) : 세로로 이어붙이기.
> columns 가 같아야 한다. 

### 그래프 그리기 

레이어로 층을 쌓아간다. 

+ 산점도 : 점으로 표현. 두 변수간의 관계를 표현할 때 사용
	+ ggplot에서는 함수 연결할때 +를 사용
	+ geom_point() : 그래프 종류 부분 (점찍기)
	+ xlim : x값 한정
	+ ylim : y값 한정
+ 막대그래프
	+ 빈도 그래프 : 개수를 세서 비교
	+ ggplot(data = mpg, aes(x = drv)) + geom_bar() 
	+ 평균그래프 : 평균 비교
		+ 집단별 평균 표를 만들고 그 표를 바탕으로 그래프 생성
		+ ggplot(data = df_mpg, aes(x=drv, y=mean_hwy)) + geom_col()	
		
+ 선그래프
+ 
시계열 데이터를 선으로 표현한 그래프. 시간에 따라 달라지는 data에 사용.

+ 날짜와 실업자 수
	+ ggplot(data = economics, aes(x= date, y=unemploy)) + geom_line()
+ 상자 그림
	+ 중앙 값이 가운데 선, 밑면은 1분위수, 윗면은 3분위수.
	+ 점으로 표현된 것은 극단치.
		+ 1분위수와 3분위 수의 거리를 구해서 1.5를 곱한다. 이보다 멀면 극단치라고 하는 것.
	+ 박스가 좁다는 건 중앙값에 몰려있는 것. 박스가 크면 다양하게 분포한다는 것이다.
	+ 평균은 극단치까지 반영하기 때문에 박스 그림이 더 좋다.
	
## 확장 그래프 찾기

+ ggplot2 extension
+ plotly 패키지 : ggplotly(p) -> 상호작용할 수 있는 그래프의 형태로 만들어준다.

## 데이터 정제하기

이상치나 빈값을 제거해주는 것이다.

+ 결측치 : 비어있는 값. 제거 후 분석 or 빈 값을 오차가 적은 다른하나의 값으로 대체 (평균 같은) or 빈값을 추정하는 회귀 모형 사용.
> NA라는 값이 결측치 : 비어있다! 

+ 이상치 : 논리적으로 존재할 수 없는 값 or 극단적인 값.
	+ 결측처리.
	+ 정상범위 기준 정해서 결측처리.
	+ 표준편차 구해서 3표준편차 이상이하면 결측처리.
	+ 상자그림으로 밑면 윗면 파악하여 범위 제한.