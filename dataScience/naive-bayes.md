## Naive Bayes

##### 나이브 가정
독립 변수 x가 다차원이면, 즉 x = (x<sub>1</sub>, ... , x<sub>D</sub>)이면 likelihood P(x|y=C<sub>k</sub>)로 모든 x = (x<sub>1</sub>, ... , x<sub>D</sub>)에 대한 결합 확률(joint probability) P(x<sub>1</sub>, ... , x<sub>D</sub> | y=C<sub>k</sub>)를 사용해야한다. 그러나 차원이 높아질 수록 결합 확률을 구하기 어렵기 때문에 모든 차원의 개별 독립 변수 요소들이 서로 조건부 독립(Conditional Independent)라는 가정을 사용한다. 이러한 가정을 적용한 모형을 **나이브 베이브 분류 모형(Naive Bayes Classification Model)** 이라고 한다.

- 모형 종류
  - 베르누이 likelihood 모형
  - 다항 분포 likelihood 모형
  - 가우시안 정규 분포 나이브 베이즈 모형

```python
from sklearn.naive_bayes import BernoulliNB
model_bern = BernoulliNB().fit(X, y)

from sklearn.naive_bayes import MultinomialNB
model_mult = MultinomialNB().fit(X, y)

from sklearn.naive_bayes import GaussianNB
model_norm = GaussianNB().fit(X, y)
```
