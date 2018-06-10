## Minimize a function using Sequential Least SQuares Programming

**scipy.optimize.fmin_slsqp** _(func, x0, eqcons=[], f_eqcons=None, ieqcons=[], f_ieqcons=None, bounds=[], fprime=None, fprime_eqcons=None, fprime_ieqcons=None, args=(), iter=100, acc=1e-06, iprint=1, disp=None, full_output=0, epsilon=1.4901161193847656e-08)_
함수를 사용하여, 제한조건이 있는 최적화 문제 **(constrained optimization)** 를 해결할 수 있다.
<br>
[링크](https://docs.scipy.org/doc/scipy-0.13.0/reference/generated/scipy.optimize.fmin_slsqp.html)
<br>

아래는 제한조건식이 여러개(4개)인 경우인데, 제한조건식 안에도 k라는 변수를 넣고, 변화시키며 최소값을 확인해가는 방법을 구현한 것이다. 이때, k의 값을 변화시키는 방법을 난 외부에 k변수를 두고 for문에서 변경시키도록 했다. 왜냐하면 fmin_slsqp()함수의 argument에 해당하는 ieqcons=[ieq_constraint]는 사용되는 함수명만 넣게끔되어있고, 내가 원했듯 k의 값을 넣는 방법을 알 수 없었기 때문이다. 확인해보니 args=()라는 argument에 전달할 수 있을듯하여 시도하였으나, 그걸 통해서 넣은 변수는 우리가 해결하고자하는 함수의 변수를 추가해서 넣을때나, fprime 에 들어가는 함수의 매개변수로 넣을 변수들을 넣는 공간이어서 결국 외부변수를 사용한 것이 그나마 절충안이라 확인하였다.
<br>
```Python
def f2(x):
    return np.sqrt((x[0] - 4) ** 2 + (x[1] - 2) ** 2)

k = 10
li = []

def ieq_constraint(x):
    # print("x, k : {}{}".format(x, k))
    return np.atleast_1d(k - np.sum(np.abs(x)))

for _ in range(20):
    a, b = sp.optimize.fmin_slsqp(f2, np.array([0, 0]), ieqcons=[ieq_constraint], iprint=0)
    print(str(round(k,2)) + " : ", end="")
    print(a, b)
    li.append((a, b))
    if k <= 1:
        k -= 0.1
    else:
        k -= 1
    # time.sleep(1)
```
