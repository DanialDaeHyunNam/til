## Latent Dirichlet Allocation

**LDA** 란 주어진 문서에 대하여 각 문서에 어떤 주제들이 존재하는지에 대한 확률모형이다.

### LDA Variables
- &phi;<br>
  &phi;는 k번째 토픽에 해당하는 벡터이다. 예를 들어 Topic 1일 경우에 말뭉치 전체의 단어들이 가지는 분포를 &phi;<sub>1</sub>이며, 이는 확률 분포이므로 요소들을 다 더하게되면 1이다. 아키텍쳐를 살펴보면 &phi;는 하이퍼 페러미터에 해당하는 &beta;의 영향을 받는다. 이는 토픽의 단어비중 &phi;가 디리클레분포를 따른다는 가정에의한 것이다.<br>
  예)
  |Terms|Topic1|Topic2|Topic3|
  |:--:|:--:|:--:|:--:|
  |Nirvana| 0.000|0.000|0.100|
  |Guitar | 0.250|0.100|0.000|
  |Bass   | 0.750 |0.900   |0.900|

- &theta;<br>
  &theta;는 d번째 문서가 가진 토픽 비중을 나타내는 벡터다. 전체 토픽 개수 K만큼의 Column 개수를 가지게되고, 행벡터로 볼 수 있다. 역시 하이퍼 페러미터 &alpha;의 영향을 받는다.
  예)
  |Docs|Topic1|Topic2|Topic3|
  |:--:|:--:|:--:|:--:|
  |Doc1| 0.000|0.900|0.100|
  |Doc2| 0.750|0.100|0.150|
  |Doc3| 0.350|0.200|0.450|
- z<br>
  z<sub>d, n</sub>은 d번째 문서 n번째 단어가 어떤 토픽에 해당하는지를 할당한다. 위의 예를 따른다면 세번째 문장의 첫 번째 단어는 Topic3일 확률이 높다.
  Topic1, Topic2, Topic3 각각 확률이 0.350, 0.200, 0.450이므로.
- w<br>
  w<sub>d, n</sub>은 문서에 등장하는 단어를 할당해주는 역할을 한다. 이는 &phi;와 z<sub>d, n</sub>의 영향을 동시에 받는다. 위의 예처럼 z<sub>3, 1</sub>이 실제로 Topic3에 속한다고 가정하고, &phi;<sub>3</sub>을 보게되면 w<sub>3, 1</sub>은 Bass일 확률이 가장 높다.

### LDA Inference
LDA는 토픽의 단어분포와 문서의 토픽분포의 결합으로 문서 내 단어들이 생성된다고 가정한다. 즉, LDA의 inference는 실제 관찰가능한 문서 내의 단어를 이용하여 토픽의 단어분포, 문서의 토픽분포를 추정하는 과정이다.<br>
수식은 아래와 같다.<br><br>
**p(&phi;<sub>1:K</sub>, &theta;<sub>1:D</sub>, z<sub>1:D</sub>, w<sub>1:D</sub>) = &prod;p(&phi;<sub>k</sub>|&beta;)&prod;p(&theta;<sub>d</sub>|&alpha;){&prod;p(z<sub>d,n</sub>|&theta;<sub>d</sub>)p(w<sub>d,n</sub>|&theta;<sub>1:K</sub>, z<sub>d,n</sub>)}**
<br><br>
수식에서 하이퍼 패러미터에 해당하는 &alpha;&beta;와 말뭉치를 통해 관찰가능한 w<sub>d,n</sub>을 제외한 모든 변수가 미지수가 된다. 우리의 목표는 **p(z, &phi; &theta; | w)** 를 최대로 만드는 z, &phi;, &theta;를 찾아야한다. 이것이 LDA의 추론이다. 분모에 해당하는 p(w)를 단번에 구할 수 없기 때문에 [gibbs sampling](gibbs-sampling.md) 기법을 사용하여야 한다.

### LDA Gibbs Sampling
LDA에서는 Collapsed gibbs sampling 기법을 사용한다. p(z, &phi;, &theta; | w)를 구할 때, &phi;, &theta;를 계산에서 생략한다.<br>
수식은<br><br>
**p(z<sub>i</sub> = j|z<sub>-i</sub>, w)**
<br><br>
수식의 의미는 단어 w와 그 단어를 제외한 문서의 모든 단어의 토픽 정보를 의미하는 z<sub>-i</sub>이 주어지면, i번째 단어의 토픽이 j일 확률을 말한다. 처음에는 문서내의 모든 단어들에 대하여 랜덤한 토픽 번호를 주어준 후에 단어를 하나씩 지우면서 깁스 샘플링을 반복하면 최종적으로 모든 단어에 대한 토픽 할당 정보가 수렴된다.<br><br>
보통 1000회~ 1만회를 반복 수행하면 수렴한다고 한다.

### 디리클레 페러미터의 역할
**p(z<sub>d,i</sub> = j|z<sub>-i</sub>, w) = (n<sub>d,k</sub> + &alpha;<sub>k</sub>)/&Sigma;(n<sub>d,i</sub> + &alpha;<sub>i</sub>) * (v<sub>k,w<sub>d,n</sub></sub> + &beta;<sub>w<sub>d,n</sub></sub>)/&Sigma;(v<sub>k,j</sub> + &beta;<sub>j</sub>) = AB**<br><br>
&alpha;와 &beta;는 극단적으로 확률분포가 쏠리는 현상을 방지하는 스무딩역할을 하게된다. 즉 값이 클수록 모든 토픽들의 분포가 비슷해지고, 작을수록 특정 토픽이 크게 나타나게 된다. 최적의 토픽을 찾기위해서는 **Perplexity** 지표를 이용한다. Perplexity값이 작을수록 좋다. 토픽 수 K를 바궈가면서 Perplexity를 구한 뒤 가장 작은 값을 내는 K를 최적의 토픽수로 삼으면 된다.



## Reference
[Link](https://ratsgo.github.io/from%20frequency%20to%20semantics/2017/06/01/LDA/)
