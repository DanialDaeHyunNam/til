## Integration In Python Using Sympy Module

```python
import sympy as sp

# 부정적분
x, y = sp.symbols('x y')
f = x ** 3 - 1
f_ = 5 * x + y

sp.integrate(f)
sp.integrate(f_, x) // x로 적분
sp.integrate(f_, y) // y로 적분

# 정적분
# 부정적분한 후에 변수에 숫자를 대입하여 계산하는 방법

# subs.evalf() is the slowest but simplest option.
# It runs at SymPy speeds.
# You should use this method production only if performance is not an issue.

F = sp.integrate(f)
(F.subs(x, 2) - F.subs(x, 0)).evalf()

# 수치 적분(Numerical integration)
sp.integrate.quad(f, 0, 2)
```
