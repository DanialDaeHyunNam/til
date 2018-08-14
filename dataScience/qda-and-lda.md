## QDA and LDA

- [Generative Model](#generativemodel)
- [QDA](#qda)
- [LDA](#lda)

**QDA(Quadratic Discriminant Analysis)** 와 **LDA(Linear Discriminant Analysis)** 는 대표적인 확률론적 생성 모형 **(Generative Model)** 이다.<br>
## GenerativeModel
생성 모형이 공부하면서 가장 흥미로운 부분이었다. 간단한 설명을 하자면, 폐암에 걸린 환자의 차트와 정상인 사람의 차트를 잘알고 있는 의사라면, 그 것을 가짜로 만들어낼 수 있다는 점을 의미한다. 베이즈 정리에서 우도에 해당하는 **p(x|y=C<sub>k</sub>)** 를 이용하면 그것이 가능해지는 것이다.<br>
다시 베이즈 정리를 살펴보자면<br>
**P(y=C<sub>k</sub>|x) = P(x|y=C<sub>k</sub>)P(y=C<sub>k</sub>)/P(x)**<br>
분류 문제를 풀때는 각 클래스 K에 대한 확률을 비교하여 가장 큰 값을 선택하는 것이기에 모든 클래스에 대해 같은 값인 분모 P(x)는 굳이 계산하지 않아도 된다.<br>
Prior 확률 P(y=C<sub>k</sub>)은 특별한 정보가 없는 경우에는<br>
**P(y=C<sub>k</sub>) &tilde; y=C<sub>k</sub>인 데이터의 수/모든 데이터의 수** 로 계산한다.<br>
y에 대한 x의 조건부 확률인 likelihood는 일반적으로 정규 분포나 베르누이 분포와 같은 특정한 모형을 가정하여 다음과 같이 계산한다.<br>
- P(x|y=C<sub>k</sub>)가 특정한 확률 분포를 따른다고 가정한다.
- k번째 클래스에 해당하는 데이터 {x1, ... xN}을 사용하여 이 모형의 모수 값을 구한다.
- 모수값을 알고 있으므로 p(x|y=C<sub>k</sub>)의 확률 밀도 함수를 구한 것이다. 즉, 새로운 독립 변수 값 x이 어떤 값이 되더라도 p(x|y=C<sub>k</sub>)의 값을 계산할 수 있다.

## QDA
QDA는 독립 변수 x가 실수이고 확률 분포가 다변수 가우시안 정규 분포라고 가정한다. 단 x분포의 위치와 형태는 **클래스에 따라 p(x|y=k)** 달라질 수 있다.<br>
이 분포들을 알고 있으면 독립 변수 x에 대한 y 클래스의 조건부 확률 분포(타겟 데이터)는 베이즈 정리와 전체 확률의 법칙으로 구할 수 있다.
```python
from sklearn.discriminant_analysis import QuadraticDiscriminantAnalysis

qda = QuadraticDiscriminantAnalysis(store_covariance=True).fit(X, y)

# qda.means_ : 각 클래스 k에서 x의 기댓값 벡터의 추정치 벡터
# qda.covariance_ : 각 클래스 k에서 x의 공분산 행렬의 추정치 행렬.
```

## LDA
**LDA** 에서는 각 Y 클래스에 대한 독립 변수 X의 조건부 확률 분포가 공통된 공분산 행렬을 가지는 다변수 가우시안 정규 분포 **(Multivariate Gaussian Normal Distribution)** 이라고 가정한다.
<br>
아래에 링크를 참조하면 증명을 볼 수 있는데, 간단하게 결론을 설명하자면 각 클래스간의 경계선이 LDA를 이용하게되면 직선이 된다는 특징이 있다.

```python
from sklearn.discriminant_analysis import LinearDiscriminantAnalysis

lda = LinearDiscriminantAnalysis(n_co   solver="svd", store_covariance=True).fit(X, y)

# 모델의 사용되는 메서드는 qda와 동일하다.
```
