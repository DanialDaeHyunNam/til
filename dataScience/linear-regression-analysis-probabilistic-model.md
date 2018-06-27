## Linear regression analysis - Probabilistic Model

- [OLS Results](#ols_results)

**statsmodels.api** 의 함수 **OLS** 에 종속변수 벡터와 독립변수 매트릭스를 입력하여 얻은 **model** 에서 **fit** 함수를 통해 리턴 받는 **result** 에는 회귀 분석 보고서를 받아올 수 있는 **summary** 라는 함수가 있다.<br>
그 보고서 상에 표시되는 수치들을 이해하기 위해서는 확률론적 **선형회귀모형(Probabilistic Model)** 을 이해해야한다.
<br>
##### 가장 큰 차이점은 확률론적 선형회귀모형은 데이터가 확률 변수로부터 생성된 표본이라고 가정한다는 점이다. 구체적 가정은 다음과 같다.
- 오차의 분포에 대한 가정
  - 선형 정규 분포 가정<br>
    **p(&epsilon; | &theta;) ~ N(0, &sigma;<sup>2</sup>)**<br>
    _**주의하셔야할 점은 x, y는 정규 분포일 필요가 없다는 점입니다.**_
  - 외생성 가정<br>
    오차 &epsilon;의 기댓값 독립변수 x의 크기에 상관없이 항상 0이라고 가정한다.
  - 조건부 독립 가정<br>
    오차는 서로 독립이다.<br>
    **Cov[&epsilon;] = &sigma;<sup>2</sup>I**
- 독립 변수에 대한 가정<br>
  독립 변수의 특징행렬은 full rank이어야 한다.

##### MLE를 사용한 선형 회귀 분석
**MLE(Maximum Likelihood Estimation)** 을 사용하여 가중치 벡터 w의 값을 구해보면 OLS와 동일한 결과를 얻을 수 있다.<br>
**w = (X<sup>T</sup>X)<sup>-1</sup>X**

##### 잔차의 분포
**e = y - w<sup>T</sup>X** 도 정규 분포를 따른다.<br>
아직 이해는 잘 가지않는 부분이지만 중요해보이는 부분은 **잔차는 e는 &epsilon;의 선형 변환이다.(오차 &epsilon;은 정규 분포이므로 선형 변환은 마찬가지로 정규 분포이다.)** 라는 점이다.

## OLS_Results
- F-statistics, Prob(F-statistics) : 독립 변수 중 어느것도 의미 가진 것이 없다는 확률을 확인하는 **Loss-of-Fit 검정(회귀 분석 F-검정)** 값이다.
- std err : **&radic;Var[w<sub>i</sub>] = &radic;s<sup>2</sup>((X<sup>T</sup>X)<sup>-1</sup>)<sub>ii</sub>(i = 0, ... , K-1)**
- t : 정규화된 모수 오차는 자유도가 N-K인 표준 스튜던트 t분포를 따른다.
- P > |t| : w가 0이다(즉, 관련이 없는 독립변수다.). 라는 귀무가설에대한 p-value이다.
- [0.025 0.975] : 95% 신뢰구간을 표현한다. 해당 독립변수의 가중치가 0.025 아래에 표기된 수치부터 0.975 아래에 표기된 수치사이에서 나올 확률이 95%라는 뜻.
