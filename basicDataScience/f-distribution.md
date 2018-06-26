## F distribution
F 분포 **(F distribution)** 는 카이 제곱 분포를 따르는 독립적인 두 개의 확률 변수의 샘플로부터 생성할 수 있다. 두 카이 제곱 분포의 샘플을 각각 x<sub>1</sub>, x<sub>2</sub>라고 할 때, 이를 n<sub>1</sub>, n<sub>2</sub>로 나누어 그 비율을 구하면 F(n<sub>1</sub>, n<sub>2</sub>) 분포가 된다.<br>
**f(x; n<sub>1</sub>, n<sub>2</sub>) = &radic;((n<sub>1</sub>x)<sup>n<sub>1</sub></sup>n<sub>2</sub><sup>n<sub>2</sub></sup> / (n<sub>1</sub>x + n<sub>2</sub>)<sup>n<sub>1</sub> + n<sub>2</sub></sup>) / x B(n<sub>1</sub>/2, n<sub>2</sub>/2)**

```python
xx = np.linspace(0.03, 3, 1000)
plt.plot(xx, sp.stats.f(1, 1).pdf(xx), label="F(1,1)")
plt.plot(xx, sp.stats.f(5, 1).pdf(xx), label="F(5,1)")
plt.plot(xx, sp.stats.f(10, 10).pdf(xx), label="F(10,10)")
plt.legend()
plt.show()
```
