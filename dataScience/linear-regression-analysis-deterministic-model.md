## Linear regression analysis - Deterministic Model

회귀분석은 독립 변수 x와 이에 대응하는 종속 변수 y간의 관계를 정량화하는 작업이다.
<br>
목표는
<br>
**y^ = f(x) &asymp; y**
<br>
를 구해내는 것이다.
<br>
**y^ = w<sub>0</sub> + w<sub>1</sub>x<sub>1</sub> + w<sub>2</sub>x<sub>2</sub> +
... + w<sub>D</sub>x<sub>D</sub> = w<sub>0</sub> + w<sup>T</sup>x** 와 같이 x와 y간의 관계가 선형인 경우를 **선형 회귀분석(Linear regression analysis)** 라고 부른다. 여기서 w를 f(x)의 **계수(coefficient)** 이자 선형 회귀모형의 **모수(parameter)** 라고 한다.
<br>

##### 바이어스 오그멘테이션
**바이어스 오그멘테이션(bias augmentation)** 은 바이어스 값에 해당하는 것을 독립변수 벡터와 종속 변수 벡터에 추가하여 단순히 x<sub>a</sub> 또는 w<sub>a</sub>의 내적으로 표시하기 위해서 실행한다.
```python
X0, y, coef = make_regression(n_samples=100, n_features=2, bias=100, noise=10, coef=True, random_state=1)

# 바이어스 오그멘테이션
X = np.hstack([np.ones((X0.shape[0], 1)), X0])
X[:5]

# 위와 같은 결과지만 간단한 방법은 statsmodels.api 패키지의 add_constant함수를 사용하는 것이다.
import statsmodels.api as sm

X = sm.add_constant(X0)
X[:5]

```
##### OLS
**OLS(Ordinary Least Squares)** 는 가중치 벡터를 행렬 미분으로 구하는 방법이다.<br>
**독립 변수들이 서로 선형 독립이면 X<sup>T</sup>X가 양한정이고 OLS의 해가 존재한다.**
<br>

##### 직교 방정식(Normal equation)

**원래 데이터를 사용한 회귀 분석 결과와 원래 데이터에서 평균이 0이 되게 평균 이동을 한 데이터를 사용한 회귀 분석 결과가 같다**
