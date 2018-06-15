## Binomial distribution

##### Understanding of python codes commonly used
- [sns.barplot](#barplot)
- [sns.countplot](#countplot)

**이항 분포** 는 0, 1 두 가지 값 중 하나만 가질 수 있는 베르누이 시도를 N번 하여 성공한 횟수를 확률 변수 X로 한다. 따라서 확률 질량 함수(pmf: probability mass function)는<br>
**X ~ Bin(x;N, &theta;) = ( <sup>N</sup><sub>x</sub> ) &theta;<sup>x</sup>(1-&theta;)<sup>N-x</sup>** <br>
그 중, **( <sup>N</sup><sub>x</sub> )** 는 combination으로 다음 공식으로 계산한다.<br>
**( <sup>N</sup><sub>x</sub> ) = N! / x!(N-x)!**<br>
**베르누이 시도는 이항 분포의 N = 1인 특수 상황이라고 볼 수 있다.**

기댓값은 **E[X] = N*&theta;**<br>
분산은 **Var[X] = N\*&theta;(1-&theta;)**<br>

**이 분포는 다음과 같은 경우에 사용된다.**

- 참이거나 거짓 중 하나만 결정되는 같은 종류의 일들이 동시에 일어날 확률을 알아볼 때

이항 분포 모형의 pmf식은<br>
**X ~ Bin(x;&theta;) = &theta;<sup>x</sup>(1-&theta;)<sup>1-x</sup>** 으로 표현된다.
<br>
베르누이 분포의 특성상 모수를 추측하는 방법은 **&Sigma;N<sub>1</sub>(x = 1인 경우가 나온 총 수)/전체의 시도 수(N)** 으로 간단하게 추정이 가능하다.

##### barplot
```python
import seaborn as sns

sns.barplot(x="x축 타이틀", y="y축 타이틀", hue="속한 데이터 타이틀", data = df)

# 주로 이산적으로 분포한 데이터들을 같은 종목끼리 비교하는 것에 사용하면 아주 유용해보이는 plot.
```

##### countplot
```python
x = array([ 6,  5,  6,  6,  6,  5,  6,  4,  3,  6,  5,  6,  6,  4,  8,  8,  9,
        5,  5,  4,  3,  5,  6,  5,  8,  5,  8,  4,  6,  6,  7,  5,  6,  6,
        9,  6,  6,  6,  4,  5,  7,  6,  5,  8,  5,  5,  7,  8,  7,  7,  6,
        6,  2,  8,  7,  8,  5,  7,  6,  7,  8,  8,  5,  8,  7,  7,  5,  8,
        4,  8,  3,  6,  3,  6,  5,  9,  7,  8,  7,  8,  7,  6,  8,  5,  6,
        7,  6,  8,  6,  4,  7,  5,  8,  5,  7,  7,  6,  9,  5, 10])

sns.countplot(x)
plt.title("이항 분포의 시뮬레이션")
plt.xlabel("표본값")
plt.show()

# bincount를 visualize한 모습이다. x축은 나온 데이터의 값이고 y축은 그 값이 나온 횟수를 높이로 보여준다.
```
