## Gaussian-mixuture model

##### 가우시안 혼합 모형
실수값을 출력하는 확률변수 X가 사실 눈에 보이지 않는 K-클래스 카테고리 확률변수 Z의 값에 따라 다른 기댓값과 분산을 가지는 복수의 가우시안 정규 분포들로 이루어진 **가우시안 혼합 모형(Gaussian Mixture)** 이라고 한다.<br>
**p(x) = &Sigma;p(z)p(x|z) = &Sigma;&theta;<sub>k</sub>N(x|&mu;<sub>k</sub>, &Sigma;<sub>k</sub>)**

- p(x) : 전체분포
- p(x|z) : 혼합 모형의 각 성분이 되는 개별적인 연속 확률분포. 여기서는 가우시안 정규 분포.
- p(z) : 카테고리 확률분포
- &theta;<sub>k</sub> : 카테고리 확률분포의 모수. 모든 성분 중 특정한 Z가 선택될 확률
- &Sigma;&theta;<sub>k</sub> = 1 : 카테고리 확률분포의 모수 제한 조건

```python
from numpy.random import randn

n_samples = 500

mu1 = np.array([0, 0])
mu2 = np.array([-6, 3])
sigma1 = np.array([[0., -0.1], [1.7, .4]])
sigma2 = np.eye(2)

np.random.seed(0)
X = np.r_[1.0 * np.dot(randn(n_samples, 2), sigma1) + mu1,
          0.7 * np.dot(randn(n_samples, 2), sigma2) + mu2,
         ]
plt.scatter(X[:, 0], X[:, 1], s=5)
plt.show()
```
