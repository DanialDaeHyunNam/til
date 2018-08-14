- [Entropy](#entropy)
- [Gini impurity](#giniimpurity)
- [Decision Tree](#decisiontree)

### Entropy
**H[Y] = -&Sigma;p(y<sub>k</sub>)log<sub>2</sub>p(y<sub>k</sub>)**<br>
확률 분포들이 가지는 확신의 정도를 수치로 표현하는 것을 엔트로피(Entropy)라고 한다. 확률 변수의 여러가지 값이 나올 확률이 대부분 **비슷한 경우에는 엔트로피가 높아지고**, 반대로 **특정한 값이 나올 확률이 높아지고 나머지 값의 확률은 낮아진다면 엔트로피가 작아진다.** <br>
물리학에서는 상태가 분산되어 있는 정도를 엔트로피로 정의한다. 고루 분산되어 있을 수 있으면 엔트로피가 높고 특정한 하나의 상태로 몰려있으면 엔트로피가 낮다.

```python
import numpy as np
-0.5 * np.log2(0.5) - 0.5 * np.log2(0.5)
```

- 조건부 엔트로피
예:) **H[Y|X<sub>1</sub>] = p(X<sub>1</sub> = 0)H[Y|X<sub>1</sub> = 0] + p(X<sub>1</sub> = 1)H[Y|X<sub>1</sub> = 1]**
- 크로스 엔트로피
예:) **H[p,q] = -&Sigma;p(y<sub>k</sub>)log<sub>2</sub>q(y<sub>k</sub>)**<br>
이 값은 주로 분류 문제의 목표값 분포와 예측값 분포를 비교하는데 사용된다.

### GiniImpurity
엔트로피와 유사한 개녀으로 지니 불순도라는 것이 있다. 지니 불순도는 엔트로피처럼 확률 분포가 어느쪽에 치우쳐있는가를 재는 척도지만 로그를 사용하지 않음으로써 계산량을 줄였다.(대부분 Gini impurity를 Default로 사용한다.)<br>
**G[Y] = &Sigma;p(y<sub>k</sub>)(1-p(y<sub>k</sub>))**

### DecisionTree
**의사 결정 나무(Decision Tree)** 는 여러 가지 규칙을 순차적으로 적용하면서 독립 변수 공간을 분할하는 모형이다.<br>
분류법은 다음과 같다.
1. 여러가지 독립 변수 중 하나의 독립 변수를 선택하고 그 독립 변수에 대한 기준값을 정한다.
2. 전체 학습데이터 집합을 해당 독립 변수의 값이 기준값보다 작은 데이터 그룹과 해당 독립 변수의 값이 기준값보다 큰 데이터 그룹으로 나눈다.
3. 각각의 자식 노드에 대해 1 ~ 2 단계를 반복하여 하위의 자식 노드를 만든다. 단, 자식 노드에 한가지 클래스의 데이터만 존재한다면 더 이상 자식 노드를 나누지 않고 중지한다.

[참조 링크(Reference)](https://datascienceschool.net/view-notebook/16c28c8c192147bfb3d4059474209e0a/)

##### 규칙 결정 방법
**정보 획득량** 이 X라는 조건에 의해 Y의 엔트로피가 얼마나 감소하였는가를 나타내는 값이다. 의사 결정 나무는 정보 획득량이 가장 많은 방향으로 나아가는 것을 규칙으로 한다.<br>
**IG[Y, X] = H[Y] - H[Y|X]**

```python
from sklearn.datasets import load_iris

iris = load_iris()
X = iris.data[:, [2, 3]]
y = iris.target

from sklearn.tree import DecisionTreeClassifier

tree1 = DecisionTreeClassifier(criterion='entropy', max_depth=1, random_state=0).fit(X, y)
```
