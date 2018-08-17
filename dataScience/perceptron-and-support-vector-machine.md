## Perceptron And Support Vector Machine

List
- [Perceptron](#perceptron)
- [Support Vector Machine](#svm)
- [Kernel SVM](#kernelsvm)

## Perceptron
**퍼셉트론** 은 가장 오래된 판별 함수 기반 예측 모형이다.<br>

퍼셉트론은 입력 x=(1, x<sub>1</sub>, ... , x<sub>m</sub>) 에 대해 1 또는 -1의 값을 가지는 y를 출력하는 비선형 함수이다. 1을 포함하는 입력 요소 x<sub>i</sub>에 대해 가중치 w<sub>i</sub>를 곱한 값이 판별 함수 f(x)가 된다.<br>
**f(x) = w<sup>T</sup>x**<br>
판별 함수 값이 활성화 함수(activation function)a(z)를 지나면 분류 결과를 나타내는 출력 y가 된다.<br>
<br>
#### 퍼셉트론 손실함수
**E(w) = -&Sigma;w<sup>T</sup>x<sub>i</sub>y<sub>i</sub>**<br>
가중치 계산은 **gradient descent** 방법을 사용한다.<br>
하지만, 퍼셉트론이 나온 시절에 컴퓨터는 현재대비 계산능력이 매우 떨어졌기 때문에, **SGD(Stochastic Gradient Descent)** 방식을 사용해서 최적화를 했다. 이는 minibatch size라하는 표본 데이터의 갯수를 실제 표본보다 줄여서 가중치를 조절하는 시기를 결정하는 방법인데, 퍼셉트론은 극단적으로 minibatch size = 1을 사용했었다(당연히 성능이 떨어진다). 샘플은 임의의 샘플을 사용하였다.
```python
from sklearn.linear_model import Perceptron
model = Perceptron(max_iter=n, eta0=0.1, random_state=1).fit(X, y)
```

## SVM
퍼셉트론 기반의 모형으로 가장 안정적인 경계선을 찾기 위한 제한 조건이 추가된 모형이다.<br>
각 클래스별로 군집한 데이터들 중에서 가장 최전방(most front)에 있는 데이터를 **서포트 벡터(Support Vector)** 라고 하며, 이 서포트 벡터들에 대해서 아래 식들이 성립해야한다.<br><br>
**f(x<sup>+</sup>) = w<sup>T</sup>x<sup>+</sup> - w<sub>0</sub> > 0** <br>
**f(x<sup>-</sup>) = w<sup>T</sup>x<sup>0</sup> - w<sub>0</sub> < 0** <br><br>
서포트에 대한 판별 함수의 값은 부호 조건만 지키면 어떤 값이 되어도 괜찮으므로, <br><br>
**w<sup>T</sup>x<sup>+</sup> - w<sub>0</sub> >= 1** <br>
**w<sup>T</sup>x<sup>0</sup> - w<sub>0</sub> <= -1**
<br><br>
의 식이 성립된다. 판별 경계선과 점 x<sup>+</sup>, x<sup>-</sup> 사이의 거리는 다음과 같이 계산할 수 있다.<br>
**(w<sup>T</sup>x<sup>+</sup> - w<sub>0</sub>) / ||w|| = 1 / ||w||**<br>
**- (w<sup>T</sup>x<sup>-</sup> - w<sub>0</sub>) / ||w|| = 1 / ||w||**<br>
이 거리의 합을 **마진(Margin)** 이라고 하며 마진값이 클 수록 더 경계선이 안정적이라고 볼 수 있다. **마진 값이 클 수록 새로운 값을 예측할 때 유리해지므로 우리의 목표는 마진값을 크게하는 것이다**. 그러므로, 우리가 최소화할 목적함수는<br>
**L = 1/2 ||w||<sup>2</sup> = 1/2 w<sup>T</sup>w**<br>
또한 모든 표본 데이터에 대해 분류를 할 수 있도록 조건이 있는 최적화 문제를 풀어야한다.<br>
라그랑주 승수법을 사용하여 최소화 목적함수를 쓰게되면,<br>
**L = 1/2 w<sup>T</sup>w - &Sigma;&lambda;<sub>i</sub>{y<sub>i</sub>(w<sup>T</sup>x<sub>i</sub> - w<sub>0</sub>) - 1}**<br>
이 최적화 문제를 풀면 w, w<sub>0</sub>, &lambda;를 얻을 수 있다. KKT(Karush-Kuhn-Tucker) 조건에서 라그랑주 승수 방법과 비슷하지만 조건을 만족시킬 필요가 없는 경우, (w<sup>T</sup>x<sub>i</sub>-w<sub>0</sub>) - 1 &ne; 0인 경우에는 a = 0이 된다.<br>
자세한 증명은 매우 복잡하므로 필요할 시에는 아래에 참조 링크에서 확인하도록 하자. 최종적으로 얻게되는 식은<br>
**f(x) = a<sup>+</sup>x<sup>T</sup>x<sup>+</sup> - a<sup>-</sup>x<sup>T</sup>x<sup>-</sup> - w<sub>0</sub>**<br>
이며, 여기에서 x<sup>T</sup>x<sup>+</sup>는 x와 x<sup>+</sup>사이의 코사인 유사도와 x 및 x<sup>-</sup>사이의 코사인 유사도이므로 결국 두 서포트 벡터와의 유사도를 측정해서 값이 큰 쪽으로 판별하게 되는 것이다.
```python
from sklearn.svm import SVC
model = SVC(kernel='linear', C=1e10).fit(X, y)
```
위 식에서 C는 **슬랙 변수(Slack variable)** 를 제한하는 역할을 하는 변수인데, 슬랙 변수가 사용되는 이유는 선형 분리가 불가능한 경우에 어느정도의 오차를 허용하기 위함이다. 하지만, 너무 커지게되면 오분류된것을 다 허용하게되어 분류가 무의미해지므로 이 슬랙변수조차 커지는 것을 방어하는 방어막이 필요한데, 그 변수가 바로 C이다. 식으로 확인하자면,<br>
**L = 1/2 w<sup>T</sup>w - &Sigma;&lambda;<sub>i</sub>{y<sub>i</sub>(w<sup>T</sup>x<sub>i</sub> - w<sub>0</sub>) - 1 + &xi;<sub>i</sub>} - &Sigma;&mu;<sub>i</sub>&xi;<sub>i</sub> + C&Sigma;&xi;<sub>i</sub>**<br>
이다.

## KernelSVM
퍼셉트론이나 서포트 벡터 머신은 선형 판별 함수 기반 모형이므로 XOR 문제를 풀지 못한다는 단점이 있다. 이를 해결하기위해 커널을 사용한다.<br>
많이 사용되는 커널은
- 다항 커널 (Polynomial Kernel))<br>
  **k(x<sub>1</sub>, x<sub>2</sub>) = (&gamma;(x<sub>1</sub><sup>T</sup>x<sub>2</sub>) + &theta;)<sup>d</sup>**
- RBF(Radial Basis Function) 또는 가우시안 커널(Gaussian Kernel))<br>
 **k(x<sub>1</sub>, x<sub>2</sub>) = exp(-&gamma;||x<sub>1</sub> - x<sub>2</sub>||<sup>2</sup>) + &theta;)**
- 시그모이드 커널(Sigmoid Kernel)<br>
 **k(x<sub>1</sub>, x<sub>2</sub>) = tanh(&gamma;(x<sub>1</sub><sup>T</sup>x<sub>2</sub>) + &theta;)**

## Reference
[서포트 벡터 머신](https://datascienceschool.net/view-notebook/6c6d450cb2ee49558856fd924b326e00/)
[커널 서포트 벡터 머신](https://datascienceschool.net/view-notebook/69278a5de79449019ad1f51a614ef87c/)
