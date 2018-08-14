## Gradient Boosting Classifier
- [에이다 부스트(Ada Boost)](#adaboost)
- [그래디언트 부스트(Gradient Boost)](#gradientboost)
- [XGBoost Library](#xgboost)

## AdaBoost
에이다 부스트와 같은 **부스트 방법은 미리 정해진 모형 집합을 사용하는 것이 아니다.** 단계별로 모형 집합에 포함할 개별 모형을 **선택** 한다. 부스팅 방법에서는 성능이 떨어지는 개별 모형을 **weak classifier** 라고 한다.<br>
최종 분류를 위한 개별 모형의 집합은 위원회(Commitee) C라고 한다. 위원회 C는 다수결 방법을 사용하지 않고 각각의 개별 모형의 출력을 다음처럼 가중 선형 결합한 값을 판별 함수로 사용한다.<br>
**C<sub>(m-1)</sub>(x<sub>i</sub>) = sign(a<sub>1</sub>k<sub>1</sub>(x<sub>i</sub>) + ... + a<sub>m-1</sub>k<sub>m-1</sub>(x<sub>i</sub>))** <br>
위원회의 멤버가 될 개별 모형을 선별하는 방법은 지수 손실 함수(Exponential loss function) L<sub>i</sub> 을 사용한다.<br>
**E = &Sigma;L<sub>i</sub><sup>(m)</sup> = &Sigma;e<sup>-y<sub>i</sub>C<sub>m-1</sub>(x<sub>i</sub>)</sup>** <br>

위 식에서 -y<sub>i</sub>C<sub>m-1</sub>(x<sub>i</sub>)는 기존의 위원회의 예측값이 올바른 경우에는 -1, 틀린 경우에는 +1이 되는 값이다. **m번째 멤버** 의 모든 후보에 대해 위 손실 함수를 적용하여 가장 값이 작은 후보를 m번째 멤버로 선정한다.

```python
from sklearn.ensemble import AdaBoostClassifier
model_ada = AdaBoostClassifier(DecisionTreeClassifier(max_depth=2, random_state=0),
                               algorithm="SAMME", n_estimators=100)
model_ada.fit(X, y)
```

## GradientBoost
그레디언트 부스트 모형은 최적화에 사용되는 gradient descent 방법을 응용한 모형이다. 함수 f(x)를 최소화하는 x는 다음과 같이 gradient descent 방법으로 찾을 수 있다. <br>
**x<sub>m</sub> = x<sub>m-1</sub> - a<sub>m</sub>df/dx** <br>
그레디언트 부스트 모형에서는 오차 함수 또는 손실 함수(loss function)L(y, C<sub>m-1</sub>)을 최소화하는 weak classifier k<sub>m</sub>은 **-dL(y,C<sub>m-1</sub>)/dC<sub>m-1</sub>** 임을 알 수 있다.<br>
**C<sub>m</sub> = C<sub>m-1</sub> - a<sub>m</sub>dL(y,C<sub>m-1</sub>)/dC<sub>m-1</sub> = C<sub>m-1</sub> + a<sub>m</sub>k<sub>m</sub>**<br>
따라서 그레디언트 부스트 모형은 분류/회귀 문제에 상관없이 weak 멤버 함수로 회귀 분석 모형을 사용한다. 가장 많이 사용되는 weak 모형은 의사 결정 회귀 모형 **(Decision Tree Regression Model)** 이다.
1. -dL(y,C<sub>m-1</sub>)/dC<sub>m-1</sub> 를 target으로 하는 weak classifier k<sub>m</sub>를 찾는다.
2. (y-(C<sub>m-1</sub> + a<sub>m</sub>k<sub>m</sub>))<sup>2</sup>를 최소화하는 step size a<sub>m</sub>을 찾는다.
3. C<sub>m</sub> = C<sub>m-1</sub> + a<sub>m</sub>k<sub>m</sub> 최종 모형을 갱신한다.

만약 손실함수가 오차 제곱 형태라면 gradient는 실제 target y 와 C<sub>m-1</sub>과의 차이인 잔차(residual)가 된다.<br>
**L(y, C<sub>m-1</sub>) = 1/2(y - C<sub>m-1</sub>)<sup>2</sup>**<br>

**-dL(y,C<sub>m-1</sub>)/dC<sub>m-1</sub> = y - C<sub>m-1</sub>**

```python
from sklearn.ensemble import GradientBoostingClassifier

model_grad = GradientBoostingClassifier(n_estimators=100, max_depth=2, random_state=0)
```

## XGBoost
Gradient boosting과 같은 알고리즘이지만 속도면에서 훨씬 개선된 라이브러리이다. **MS사에서 만든 LightGBM이 현재는 더 빠르고 성능이 좋다.**

```python
import xgboost

model_xgb = xgboost.XGBClassifier(n_estimators=100, max_depth=2)

model_xgb.fit(X, y)
```
