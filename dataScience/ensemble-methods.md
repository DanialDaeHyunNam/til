## Ensemble Methods
모형 결합 방법은 앙상블 방법론이라고 한다. 복수의 예측 모형을 결합하여 더 나은 성능의 예측을 하려는 시도이다.
- 최고의 장점은 단일 모형 사용할 때 보다 과최적화(Over-fitting)를 방지할 수 있다.

##### 두가지 방법론이 있다.
- 취합 방법론
  - 다수결(Majority Voting)
  - 배깅(Bagging)
  - 랜덤 포레스트(Random Froests)
- 부스팅 방법론
  - 에이다부스트(Ada Boost)
  - 그레디언트 부스트(Gradient Boost)

##### 다수결 방법
다수결 방법에는 두 가지 방법이 있다.
1. hard voting : 단순 투표
2. soft voting : 가중치 투표

```python
from sklearn.linear_model import LogisticRegression
from sklearn.naive_bayes import GaussianNB
from sklearn.discriminant_analysis import QuadraticDiscriminantAnalysis
from sklearn.ensemble import VotingClassifier

model1 = LogisticRegression(random_state=1)
model2 = QuadraticDiscriminantAnalysis()
model3 = GaussianNB()
ensemble = VotingClassifier(estimators=[('lr', model1), ('qda', model2), ('gnb', model3)],
                            voting='soft', weights=[1, 1, 2])
```
##### 배깅
모형 결합에서 사용하는 독립적인 모형의 수가 많을수록 성능 향상이 일어날 가능성이 높다. 하지만 각각 다른 모형을 사용하는데에는 한계가 있으므로 보통은 배깅을 사용한다.
- 같은 데이터 샘플을 중복사용하지 않으면 : Pasting
- 같은 데이터 샘플을 중복사용하면 : Bagging
- 데이터가 아니라 다차원 독립 변수 중 일부 차원을 선택하는 경우 : Random Subspaces
- 데이터 샘플과 독립 변수 차원 모두 일부만 랜덤하게 사용하면 : Random Patches

```python
from sklearn.datasets import load_iris
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import BaggingClassifier

iris = load_iris()
X, y = iris.data[:, [0, 2]], iris.target

model = BaggingClassifier(DecisionTreeClassifier(), bootstrap_features=True, random_state=0).fit(X, y)
```

## Random Froests
**랜덤 포레스트** 는 의사 결정 나무를 개별 모형으로 사용하는 모형 결합 방법을 말한다.<br>
배깅과 마찬가지로 데이터 샘플의 일부만 선택하여 사용한다. 차이점은 **노드 분리시** 모든 독립 변수들을 비교하여 최선의 독립 변수를 선택하지않고 랜덤하게 감소시키고 그 중 독립 변수를 선택한다. 이렇게 하면 개별 모형들간의 상관관계가 줄어 성능이 좋아진다.<br>
특히, Extremely Randomized Trees를 사용하게되면 각 노드에서 랜덤하게 독립변수를 선택한다.**(큰 이점은 Feature Importance를 계산할 수 있다는 점이다.)**

```python
from sklearn.datasets import make_classification
from sklearn.ensemble import ExtraTreesClassifier

X, y = make_classification(n_samples=1000, n_features=10, n_informative=3, n_redundant=0, n_repeated=0,
                           n_classes=2, random_state=0, shuffle=False)

forest = ExtraTreesClassifier(n_estimators=250, random_state=0)
forest.fit(X, y)

importances = forest.feature_importances_
```
