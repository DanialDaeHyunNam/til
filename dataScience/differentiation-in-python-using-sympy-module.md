## Differentiation In Python Using Sympy Module

```python
import sympy as sp

x, k, a, b = sp.symbols('x k a b')
f1 = x ** 3 - 1
f2 = sp.log(x ** 2 - 3 * k)
f3 = sp.exp(a * x ** b)

sp.diff(f1, x)
sp.simplify(sp.diff(f1, x)) # 인수분해까지 하는 경우

sp.diff(f2, x)

sp.diff(f3, x)

sp.diff(f1, x, x) # 2차 도함수

y = sp.symbols('y')
f4 = x ** 2 + 4 * x * y + 4* y ** 2
sp.diff(f4, x) # x로 편미분
sp.diff(f4, y) # y로 편미분
sp.diff(f4, y, x) # y로 편미분 후, x로 편미분
```

##### by Danial

---

## Reference
