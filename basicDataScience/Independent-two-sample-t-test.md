## Independent two sample t test

**독립 표본 t-검정(Independent two sample t-test)** 는 두 개의 독립적인 정규 분포에서 나온 두 개의 데이터 셋을 사용하여 두 정규 분포의 기댓값이 동일한지를 검사한다.

```python
N_1 = 10; mu_1 = 0; sigma_1 = 1
N_2 = 10; mu_2 = 0.5; sigma_2 = 1
np.random.seed(0)
x1 = sp.stats.norm(mu_1, sigma_1).rvs(N_1)
x2 = sp.stats.norm(mu_2, sigma_2).rvs(N_2)

sp.stats.ttest_ind(x1, x2, equal_var=True)

# output : Ttest_indResult(statistic=-0.41399685269886549, pvalue=0.68376768941164268)
# 유의 확률이 68.4%이므로 기각할 수 없다. 즉 두 분포의 평균은 같다.
# equal_var 패러미터를 통해서 분산과 관계없이 Mean값만 검증하는 것도 가능하다.
```
