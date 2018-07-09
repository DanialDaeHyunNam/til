## Binomial test

**이항 검정(Binomial test)** 는 베르누이 시도의 모수 &theta;를 검정하는 방법이다. SciPy stats의 binom_test 명령은 이항 검정의 **P-value(유의 확률)** 를 계산한다. Default hypothesis of &theta; is 0.5.
<br>
<br>
```python

'''
  동전 앞면이 나온 확률을 예로 들자면, n은 앞면이 나온 횟수이며 N은 전체 시도 횟수이다.
'''

# n은
sp.stats.binom_test(n, N)

```
전체 시도한 횟수가 늘어나게되면 샘플 평균의 분산식인 **Var[X_평균] = 1/N * Var[X]** 에의해 분산이 좁아진다. 즉 시도횟수가 많은 경우일수록 검정에서 나온 결과에대한 신뢰도가 높다는 의미이다.
