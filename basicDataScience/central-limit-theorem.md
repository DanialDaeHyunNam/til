## Central Limit Theorem

중심 극한 정리에 따르면 **정규화된 샘플 평균의 분포는 n이 증가할 수록 표준 정규 분포에 수렴** 한다.

```python
np.random.seed(0)
xx = np.linspace(-2, 2, 100)
plt.figure(figsize=(6, 9))
for i, N in enumerate([1, 2, 20]):
    # np.random.rand(5000, N) : N개의 랜덤한 값이 들어간 리스트를 5000개 만든다.
    X = np.random.rand(5000, N)
    # X.mean() : 아규먼트로 값을 넘겨주지 않는 경우에는 모든 값의 평균값을 리턴한다.
    # X.mean(axis=1) : 현재 X의 경우는 N개의 값을 가진 5000개의 리스트이다. 이 경우 각에는 리스트내의 N개에 해당하는 평균을 구하여, 5000개의 평균이 들어간 리스트를 리턴한다.
    # X.mean(axis=0) : 이 경우엔 열에 해당하는 5000개의 값을 평균한 값을 리스트에 추가하여 총 N개의 값이 들어간 리스트를 리턴한다.
    # Xbar는 중심 극한 정리를 위해 샘플 평균의 평균이 0, 분산이 1이 되도록 정규화하는 작업을 실행한 것이다.
    Xbar = (X.mean(axis=1) - 0.5) * np.sqrt(12 * N)
    ax = plt.subplot(3, 2, 2 * i + 1)
    sns.distplot(Xbar, bins=10, kde=False, norm_hist=True)
    plt.xlim(-5, 5)
    plt.yticks([])
    ax.set_title("N = {0}".format(N))
    plt.subplot(3, 2, 2 * i + 2)
    sp.stats.probplot(Xbar, plot=plt)

plt.tight_layout()
plt.show()
```
