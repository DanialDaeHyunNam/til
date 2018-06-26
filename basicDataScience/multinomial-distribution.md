## Multinomial distribution

##### Understanding of python codes commonly used
- [sns.boxplot](#boxplot)
- [sns.stripplot](#stripplot)
- [sns.violinplot](#violinplot)
- [sns.swarmplot](#swarmplot)

**다항 분포** 는 독립적인 카테고리 분포를 여러번 시도하여 얻은 각 원소의 성공횟수 값은 다항분포를 이룬다. 따라서 확률 질량 함수(pmf: probability mass function)는<br>
**Mu(x;N, &theta;) = (<sup>N</sup><sub>x</sub>) &Pi;&theta;<sup>x<sub>k</sub></sup><sub>k</sub> = ( <sup>N</sup><sub>x<sub>1</sub>, x<sub>2</sub>, . . . , x<sub>k</sub></sub>) &Pi;&theta;<sup>x<sub>k</sub></sup><sub>k</sub>** <br>
이 식에서, <br>
**( <sup>N</sup><sub>x<sub>1</sub>, x<sub>2</sub>, . . . , x<sub>k</sub></sub>) = N! / x<sub>1</sub>! ... x<sub>k</sub>!**
<br>

**카테고리 분포는 다항 분포의 N = 1인 특수 상황이라고 볼 수 있다.**

기댓값은 **E[X<sub>k</sub>] = N*&theta;<sub>k</sub>**<br>
분산은 **Var[X<sub>k</sub>] = N\*&theta;<sub>k</sub>(1-&theta;<sub>k</sub>)**<br>

**이 분포는 다음과 같은 경우에 사용된다.**

- 시도 횟수가 Fix되어 있는 경우
- 각 시도가 서로 독립적일 경우
- 오직 참 혹은 거짓만의 결과가 나오는 경우
- 성공의 확률이 매 시도마다 변하지 않는 경우
- 확률 변수 Y=성공 횟수일 경우

##### boxplot
```python
import seaborn as sns

sns.boxplot(x="x축 타이틀", y="y축 타이틀", data = df)

# 박스-휘스커 플롯이라 불리는 차트를 그려준다.
```

##### stripplot
```python
sns.stripplot(x="x축 타이틀", y="y축 타이틀", data = df, jiter = True)

#stripplot은 마치 스캐터 플롯처럼 모든 데이터를 점으로 그려준다. jitter=True를 설정하면 가로축상의 위치를 무작위로 바꾸어서 데이터의 수가 많을 경우에 겹치지 않도록 한다.
```

##### violinplot
```python
sns.violinplot(x="x축 타이틀", y="y축 타이틀", data = df)

#violinplot은 세로 방향으로 커널 밀도 히스토그램을 그려주는데 왼쪽과 오른쪽이 대칭이 되도록 하여 바이올린처럼 보인다.
```

##### swarmplot
```python
sns.swarmplot(x="x축 타이틀", y="y축 타이틀", data = df)

#swarmplot은 stripplot과 비슷하지만 데이터를 나타내는 점이 겹치지 않도록 옆으로 이동한다.
```
