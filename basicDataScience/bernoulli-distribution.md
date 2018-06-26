## Bernoulli distribution

##### Understanding of python codes
- [np.bincount](#bincount)
- [pd.DataFrame.stack](#stack)

**베르누이 변수** 는 0, 1 두 가지 값 중 하나만 가질 수 있으므로 이산 확률 변수(discrete random variable)이다. 따라서 확률 질량 함수(pmf: probability mass function)로 정의할 수 있다.

기댓값은 **E[X] = &theta;**<br>
분산은 **Var[X] = &theta;(1-&theta;)**<br>

**베르누이 분포는 다음과 같은 경우에 사용된다.**

- 분류 예측 문제의 출력 데이터가 두 가지로 구분되는 경우 어느 값이 상대적으로 확률이 높은지 표현하기 위해서

베르누이 분산 모형의 pmf식은<br>
**Bern(x;&theta;) = &theta;<sup>x</sup>(1-&theta;)<sup>1-x</sup>** 으로 표현된다.
<br>
베르누이 분포의 특성상 모수를 추측하는 방법은 **&Sigma;N<sub>1</sub>(x = 1인 경우가 나온 총 수)/전체의 시도 수(N)** 으로 간단하게 추정이 가능하다.

##### bincount
```python
import numpy as np

np.bincount(np.array([0, 1, 1, 3, 2, 1, 7]))

# Output : array([1, 3, 1, 1, 0, 0, 0, 1])
# 의미는 0이 1, 1이 3, 2가 1, 3이 1개, 4,5,6은 0, 7은 1개 들어왔다는 의미다.

# bincount에서 나오는 결과의 길이는 입력된 리스트 값 중에서
# 가장 큰 값 - 1의 길이가 나오고, 만약 minlength = 라는
# parameter값에 명시된 값은 반드시 양수여야하며 입력된 값 중에 가장 큰 값보다 클 경우에는 나머지는 결과값이 0으로 채워진다.
# 즉,

np.bincount(np.array([0, 1, 1, 3, 2, 1, 7]), minlength = 10)

# Output : array([1, 3, 1, 1, 0, 0, 0, 1, 0, 0, 0])
```

##### stack
```python
df_single_level_cols = pd.DataFrame([[0, 1], [2, 3]], index=['cat', 'dog'], columns=['weight', 'height'])

df_single_level_cols

#output
     weight height
cat       0      1
dog       2      3

#.stack()
df_single_level_cols.stack()

#output
cat  weight    0
     height    1
dog  weight    2
     height    3
dtype: int64

# 원래 데이터프레임의 컬럼을 1개로 바꾸는 역할을 한다. 컬럼에 Depth가 없었던 경우에는 Series를 반환하고,
# Depth가 존재하는 경우에는 가장 낮은 컬럼들을 합치고 상위 Depth를 컬럼으로하는 DataFrame값을 반환한다.
```
