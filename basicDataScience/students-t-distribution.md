## Student's t-distribution

##### Understanding of python codes commonly used
- [np.std](#np_std)

스튜던트 t 분포의 확률 밀도 함수는 다음 수식에 의해 정의된다.

**t(x;&mu;, &sigma;<sup>2</sup>, &nu;) = (&Gamma;((&nu; + 1)/2) / &nu;&pi;<sup>1/2</sup>&Gamma;(&nu;/2)) * (1 + (x - &mu;)<sup>2</sup>/&nu;&sigma;<sup>2</sup>)**<br>
이 식에서 &Gamma;는 감마함수라는 특수 함수이다.<br>
**&Gamma;(x) = &int;<sub>o</sub><sup>&infin;</sup> u<sup>x-1</sup>e<sup>-u</sup>du**
<br>
스튜던트 t 분포의 pdf를 그리려면 SciPy 패키지의 t명령을 사용한다. 이 때, df는 (Degree of Freedom)의 약자로 자유도를, loc는 기댓값, scale은 표준편차를 설정한다.<br>
자유도 &nu;가 작으면 가우시안 정규 분포보다 분산이 크고 fat tail을 보이지만 자유도가 증가할수록 가우시안 정규 분포로 다가서는 것을 볼 수 있다.<br>

기댓값 : **E[X] = &mu;**<br>
분산 : **Var[X] = &mu;&sigma;<sup>2</sup>/(&mu; - 2)<br>(&nu; > 2 인 경우만 적용됨. &mu; = 1, 2일 때는 분산이 무한대)**
<br>
가우시안 정규 분포로부터 얻은 n개의 샘플 x<sub>1</sub>, ... , x<sub>n</sub>로부터 얻은 샘플 평균을 샘플 표준편차로 정규화한 값은 자유도가 n-1인 스튜던트 t분포를 이루게된다.
<br>
가장 중요한 차이는 **샘플** 표준편차로 정규화를 진행하였다는 것.<br>
정규 분포로 부터 얻은 샘플 데이터의 샘플 평균은 그 자체로는 항상 정규 분포를 따르지만 샘플 표준편차라고 하는 다른 확률 변수로 나누는 과정에서 정규 분포가 아닌 스튜던트 t분포를 따르게 된다.
<br>
이 정리는 추후 정규 분포의 기댓값에 관한 각종 **검정(testing)** 에서 사용된다.

##### Statistics
복수의 샘플 데이터 집합을 수치적으로 연산하여 구한 숫자를 **통계량(Statistics)** 이라고 한다.

##### np_std

```python
numpy.std

numpy.std(a, axis=None, dtype=None, out=None, ddof=0, keepdims=<class 'numpy._globals._NoValue'>)

# 여기서 ddof는 delta degrees of freedom으로 값을 1을 넣게되면 n-1 표준편차 즉 비편향 표준편차를 구하는 것이다. 샘플 평균을 샘플 표준편차로 표준화하면 자유도가 n-1인 t분포를 얻게할 때 사용.

# student t 분포 dof 4인 경우의 예
np.random.seed(0)

rv = sp.stats.norm()
M = 1000

N = 4
x1 = rv.rvs((N, M))
xbar1 = x1.mean(axis=0)
xstd1 = x1.std(axis=0, ddof=1)
x = xbar1 / (xstd1 / np.sqrt(N))
sns.distplot(x, kde=True)
xx = np.linspace(-6, 6, 1000)
plt.plot(xx, rv.pdf(xx), 'r:', label="normal")
plt.xlim(-6, 6)
plt.ylim(0, 0.5)
plt.title("N = 4")
plt.legend()

```
