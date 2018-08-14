## Logistic Regression
로지스틱(logistic) 회귀 분석은 분류 문제와 회귀에 모두 사용될 수 있는 모델이다. 가정은 종속 변수가 이항 분포를 따르고 그 모수 &theta;가 독립변수 x에 의존한다고 가정한다.<br>
**p(y|x) = Bin(y|&theta;(x), N)**<br>
y는 (0~N) 구간내의 값만을 가진다. 즉, N = 1인 베르누이 확률분포인 경우를 예로들면 &theta; >= 0.5면 1, &theta; < 0.5 이면 0으로 분류할 수 있다.

##### 시그모이드 함수(Sigmoid function)
모수 &theta;는 x의 함수 &theta;(x)이다. 확률을 결과로 보여줘야하므로 값은 0에서 1사이의 값만 나올 수 있도록 시그모이드 함수를 사용하여 변형하여준다.
<br>
**&theta; = f(w<sup>T</sup>x)**
<br>

가장 많이 사용되는 Logistic function은<br>
**logistic(z) = &sigma;(z) = 1/(1+exp(-z))**<br>
이다. 이 외에 함수모형은 아래에서 참조한 문서의 링크를 확인하자.

```python
# 예제 코드
# sklearn에서 제공하는 LogisticRegression 메서드를 사용하면 된다.
from sklearn.linear_model import LogisticRegression

model = LogisticRegression().fit(X, y)

```


##### Reference
[데이터 사이언스 스쿨(Data science school)](https://datascienceschool.net/view-notebook/d0df94cf8dd74e8daec7983531f68dfc/)
