## Python in BOAZ

### Dictionary

- key: 변경불가
- value: 변경가능
- keys: 키값들만 가져옴
- values: value들만 가져옴
- list() 로 감싸주어 리스트로 변환가능
- dict(): dictionary로 변환 가능
- .update()로 dict끼리 더하면 된다.

###인덱스

- 역 인덱스 가능
- pop: 스택의 pop 개념
- remove: 특정 원소 삭제
- del []: 특정 원소에 있는 인덱스 삭제
- index(): 특정 원소의 인덱스 리턴
- count(): 특정 원소가 몇개있는지를 찾아
- get(): 값이 없으면 None을 반환

### 기초문법

- countinue: 반복문의 처음으로 돌아감
- Call by object reference
	- return 값이 있어야 한다.

```
def swap ( a , b ):
    return b , a
print(num1,num2)
num1,num2=swap (num1,num2)
print(num1,num2)
```



## Numpy

순서대로 메모리에 할당한다. list의 단점 보완.

### 초기화

- temp_np=np.zeros((3, 4))
> 1로 채우고 싶으면 ones

- n by n 배열

#### np.full 함수

- np.full(shape, fill_value, dtype=None, order='C')
- 지정된 shape의 배열을 생성하고, 모든 요소를 지정한 "fill_value"로 초기화
- Ex 

```
tempnp = np.full((2,2),7)
npprint(tempnp)
```

#### np.eye 함수

- np.eye(N, M=None, k=0, dtype=<class 'float'>)
- (N, N) shape의 단위 행렬(Unit Matrix)을 생성

#### like 함수

- numpy는 지정된 배열과 shape이 같은 행렬을 만드는 like 함수를 제공합니다.
- np.zeros_like
- np.ones_like
- np.full_like
- np.enpty_like
- 배열의 n*m 형태만 따온다. 

... Jupyter notebook을 보도록 하자....



## 멀티 프로세싱

- 전처리시, cpu가 하나만 돌기 때문에 여러개 돌도록 하는 것.

```
cpucnt = cpu_count() - 1
cpucount()
--> cpu 세어준다. 
```
