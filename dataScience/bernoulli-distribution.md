## Bernoulli distribution

##### Understanding of python codes
- [np.bincount](#bincount)

**베르누이 변수** 는 0, 1 두 가지 값 중 하나만 가질 수 있으므로 이산 확률 변수(discrete random variable)이다. 따라서 확률 질량 함수(pmf: probability mass function)로 정의할 수 있다.

##### bincount
```python
import numpy as np

np.bincount(np.array([0, 1, 1, 3, 2, 1, 7]))

# Output : array([1, 3, 1, 1, 0, 0, 0, 1])
# 의미는 0이 1, 1이 3, 2가 1, 3이 1개, 4,5,6은 0, 7은 1개 들어왔다는 의미다.

# bincount에서 나오는 결과의 길이는 입력된 리스트 값 중에서
# 가장 큰 값 - 1의 길이가 나오고, 만약 minlength = 라는
# parameter값에 명시된 값은 반드시 양수여야하며 입력된 값 중에 가장 큰 값보다 클 경우에는 나머지는 결과값이 0으로 채워진다.
# 즉,

np.bincount(np.array([0, 1, 1, 3, 2, 1, 7]), minlength = 10)

# Output : array([1, 3, 1, 1, 0, 0, 0, 1, 0, 0, 0])


```
