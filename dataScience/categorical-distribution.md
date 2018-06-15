## Categorical distribution

##### Understanding of python codes commonly used
- [pd.get_dummies](#get_dummies)
- [np.finfo(np.float).eps](#finfo_eps)
- [numpy.ndarray.sum()](#numpy_sum)

**카테고리 분포** 는 1부터 K까지의 정수 값 중 하나가 나오는 확률 변수의 분포이다. 카테고리는 본래 어떤 개념이 하나의 값에 분류되는 것을 목표로하여 스칼라값을 출력하는 확률 변수이지만, 보통 다음과 같이 1과 0으로만 이루어진 다차원 벡터 형태로 인코딩한 값을 출력하는 벡터 확률 변수로 사용한다. 이를 **One-Hot-Encoding** 이라 한다.<br>
조건은 <br>
**x<sub>i</sub> = 0 or 1**,<br>
**&Sigma;x<sub>n</sub> = 1** 이다. 즉, x<sub>n</sub> 중 하나만 1이라는 뜻이다.<br>
각 x<sub>n</sub>는 &theta;<sub>n</sub>값을 가진다.<br>
**0 <= &theta;<sub>n</sub> <= 1<br>&Sigma;&theta;<sub>n</sub> = 1**

**Cat(x<sub>1</sub>, x<sub>2</sub>, ..., x<sub>k</sub>;&theta;<sub>1</sub>, &theta;<sub>2</sub>, ..., &theta;<sub>k</sub>)** 으로 표기하고, pmf는<br>
**Cat(x; &theta;) = &theta;<sub>1</sub><sup>x1</sup>&theta;<sub>2</sub><sup>x2</sup> ... &theta;<sub>k</sub><sup>xk</sup>,** 이다.<br>

기댓값은 **E[X<sub>k</sub>] = &theta;<sub>k</sub>**<br>
분산은 **Var[X<sub>k</sub>] = &theta;<sub>k</sub>(1-&theta;<sub>k</sub>)**<br>

**이 분포는 다음과 같은 경우에 사용된다.**

- 대표적인 예는 주사위인데, 주사위를 던져 나오는 눈금의 수를 확률 변수라고 한다면 이 확률 변수는 {1, 2, 3, 4, 5, 6}값이 나오는 즉, 클래스의 수 K = 6인 카테고리 분포이다. 

##### get_dummies
```python
s = pd.Series(list('abca'))
pd.get_dummies(s)

  a b c
0 1 0 0
1 0 1 0
2 0 0 1
3 1 0 0

xx = np.arange(1, 7)
xx_ohe = pd.get_dummies(xx)

  1 2 3 4 5 6
0 1 0 0	0 0 0
1 0 1 0	0 0 0
2 0 0 1	0 0 0
3 0 0 0	1 0 0
4 0 0 0	0 1 0
5 0 0 0 0 0 1

# Convert categorical variable into dummy/indicator variables. 카테고리 변수들을 데이터 프레임으로 반환해준다.(기본형인듯..?)

```

##### finfo_eps
```python
eps = np.finfo(np.float).eps
theta = np.array([eps, eps, 0.1, 0.2, 0.3, 0.4])
rv = sp.stats.multinomial(1, theta)

# Categorical distribution의 각 모수값을 설정할 때, 표현가능한 가장 작은 float값을 eps를 이용해서 얻을 수 있다. 1.0 + eps != 1.0

# eps의 output은 2.220446049250313e-16

```

##### numpy_sum
```python
X = rv.rvs(100, random_state=1)
y = X.sum(axis = 0)/float(len(X))

# row를 다 더한 값을 반환한다. 벡터라고 볼 수 있다.
```
