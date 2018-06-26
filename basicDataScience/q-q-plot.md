## Q-Q plot

**Q-Q(Quantile-Quantile)** 플롯은 분석하고자 하는 샘플 데이터의 분포와 정규 분포의 분포형태를 비교하는 시각적 도구이다.
<br>
SciPy 패키지의 stats 서브 패키지에서 Q-Q 플롯을 계산하고 그리기 위한 probplot 명령을 제공한다.
<br>
**그리는 방법의 첫 번째는 대상 샘플 데이터를 정렬하는 것** 으로 시작하기 때문에, 큰 데이터의 경우 불가능하거나 속도가 많이 느릴 수 있다는 단점이 있다.

```python
np.random.seed(0)
x = np.random.randn(100)
plt.figure(figsize=(7, 7))

sp.stats.probplot(x, plot=plt)

plt.axis("equal")
plt.show()
```
