## Chi-square test

**카이 제곱 검정(Chi-square test)** 는 카테고리 분포의 모수에 대한 가설을 검정하는 방법이다. 원래 카테고리 k가 나와야 할 횟수의 기댓값 m<sub>k</sub>와 실제 나온 횟수 x<sub>k</sub>의 차이를 이용하여 다음처럼 검정 통계량을 구한다.<br>
**&Sigma;(K, k=1) (x<sub>k</sub> - m<sub>k</sub>)<sup>2</sup> / m<sub>k</sub>** <br>
Default 귀무가설은 &theta; = (1/k, ..., 1/k), k는 카테고리 개수
<br>
```python
# n은 각 카테고리별 발생한 횟수들을 인수로 갖는 list or numpy array 변수이다.
# 예) array([0, 3, 5, 2])
sp.stats.chisquare(n)
```
카이 제곱 검정은 카테고리 변수간의 상관관계를 검증할 수도 있다. 즉, X의 값이 변할 때, Y의 값도 많이 다를 경우에 상관관계 검증을 **chi2_contingency** 명령으로 검정을 수행할 수 있다.

```python
obs = np.array([[10, 10, 20], [20, 20, 20]])
sp.stats.chi2_contingency(obs)

# output : (2.7777777777777777, 0.24935220877729622, 2, array([[ 12.,  12.,  16.], [ 18.,  18.,  24.]]))
# 24.9%의 유의 확률이므로 상관 관계가 없다라는 의미다.
```
