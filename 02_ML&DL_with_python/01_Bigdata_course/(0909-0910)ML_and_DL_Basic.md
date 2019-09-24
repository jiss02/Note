## K-Means

차원마다 평균을 구해주어야하며, 피쳐가 많은 경우 오래걸려서 힘들다.

차원을 축소하거나, 센터의 수를 잘 고려하도록하자.



## 차원축소

분산을 잘설명한다는 것이 뭔가?

모든 차원에 데이터를 뿌린다고?



## pkl

데이터의 작은 뭉치



# 복습

## numpy

- np_array.dtype : 행렬을 이루는 원소들의 타입을 알려준다.
- np.arange(시작, 끝) : 시작 숫자부터 끝 숫자까지 하나씩 원소를 만들어준다.



## Pandas

- Series 데이터 : 키가 있는 리스트. 아이템마다 키값이 있다. 숫자가아닌 다른 것으로도 가능하다는 뜻이다.

- df.values : np array 형태로 값들만 가져와 준다.

- df.loc["열이름" , "열이름"] : 행이름, 열이름으로 인덱싱이 가능하다.

- df.iloc[인덱스 , 인덱스] : 인덱스 번호(숫자)로 인덱싱이 가능하다.

- df.insert( `삽입할 열`, `열이름`, `값`)

  > 새로운 열을 추가할때는 값을 리스트로 넘겨주는 것이 일반적이다.

df['열'] 에 부등호 사용이 가능하다. True False로 결과가 나오게 된다. 또한 df[ `걸고자 하는 조건` ] 의 형태를 통해 원하는 행만 뽑아낼 수 있다 (조건에 맞는 행만 뽑아내는 것이다).



df의 count열이 1보다 크거나 같고 10보다 작은 행들을 뽑아보자!

```
df = df[ (df['count'] < 10) & (df['count'] >= 1) ]
```



- df['columns'].value_counts() = 각 클래스의 총합을 알려준다.

  

### df의 열에 함수 적용하기 (apply 함수 이용)

**방법 1**

```python
def num_to_character(data):
    if data == 1:
        return 'male'
    else:
        return 'female'
       
df['gender_2'] = df['gender'].apply(num_to_character) # 적용하다
```

**방법 2** (람다 사용)

```python
df['gender_2'] = df['gender'].apply(lambda x : "male" if data == 1 else 'female')
```



- `df['gender'].value_counts().plot(kind="bar")` : 편하게 열의 그래프를 그려볼수있다.



## 통계

교차검증: 두 범주형 변수 간의 관계가 어떻게 되는지이다.

> p-값이 0.05 이하면 대립가설을 채택한다. 유의미한 차이가 있다는 것이다.

귀무가설은 디폴트.이다 _~가 없다_ 같은 느낌이며 대립가설을 우리가 실험이나 적용을 통해 이끌어 낼수 있는 결과이다.

```
ct = pd.crosstab(df.propensity, df.skin, margins=True)
```

의 코드로 가능하며, margins 인자의 경우 All 옵션을 붙여줄건지 아닌지를 결정하는 요소이다.



### 분산분석

Anova

p값이 0.05 이하이면 동일한 세개의 집단이 동일한 변수값을 가질떄 적어도 하나의 집단에는 유의미한 결과를 가진다.