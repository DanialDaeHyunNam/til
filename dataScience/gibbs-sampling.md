## Gibbs Sampling

깁스 샘플링은 마코프 연쇄에 기반한 MCMC 알고리즘의 한 예이다. 다음번에 생성될 샘플은 현재 샘플에 영향을 받는다는 점은 같지만, 차이점은 나머지 변수는 그대로 두고 한 변수에만 변화를 준다는 점이 다르다.<br>

절차는
1. 임의의표본 X<sup>0</sup> = (x<sub>1</sub><sup>0</sup>, x<sub>2</sub><sup>0</sup>, x<sub>3</sub><sup>0</sup>)을 선택한다.
2. 주어진 표본 중 x<sub>2</sub><sup>0</sup>, x<sub>3</sub><sup>0</sup>은 고정하고, p(x<sub>1</sub><sup>1</sup>|x<sub>2</sub><sup>0</sup>, x<sub>3</sub><sup>0</sup>)의 확률로 x<sub>1</sub><sup>1</sup>을 생성한다.
3. p(x<sub>2</sub><sup>1</sup>|x<sub>1</sub><sup>1</sup>, x<sub>3</sub><sup>0</sup>)로 x<sub>2</sub><sup>1</sup>를 생서하고, 똑같은 방법으로 x<sub>3</sub><sup>1</sup>까지 생성하여, X<sup>1</sup>을 구한다.<br>

새로운 값을 뽑는 것은 사용된 결합확률분포 p(x<sub>1</sub>, x<sub>2</sub>, x<sub>3</sub>)에 비례한다고 한다. 표본의 앞부분은 초기 상태에 크게 의존하지만 충분히 많이 뽑고 난 뒤에는 p에 기반한 표본을 수집하게 된다.

### Collapsed Gibbs Sampling
불필요한 일부 변수를 샘플링에서 생략하는 기법이다.


## Reference
[Link](https://ratsgo.github.io/statistics/2017/05/31/gibbs/)
