## Gaussian normal distribution

##### Understanding of python codes commonly used
- [sns.distplot](#distplot)

**가우시안 정규 분포(Gaussian normal distribution)** 은 간단하게 정규 분포라고 표현하며, 자연 현상에서 나타나는 숫자를 확률 모형으로 모형화할 때 가장 많이 사용되는 모형이다.

모수는 &mu;와 분산 &sigma;<sup>2</sup>으로 두 개이며, pdf는 다음 수식과 같다.

**N(x;&mu;, &sigma;<sup>2</sup>) = 1/(2&pi;&sigma;<sup>2</sup>)<sup>1/2</sup> * exp(-(x-&mu;)<sup>2</sup> / 2&sigma;<sup>2</sup> )**

- x = &mu; 일 때 확률 밀도가 최대가 된다.
- x = &infin; 로 다가가거나 x = -&infin;으로 다가갈수록 확률 밀도가 작아진다.


##### distplot
```python
sns.distplot(a, bins=None, hist=True, kde=True, rug=False, fit=None, hist_kws=None, kde_kws=None,/
 rug_kws=None, fit_kws=None, color=None, vertical=False,/
 norm_hist=False, axlabel=None, label=None, ax=None)

#distplot을 사용하면 scipy.stats의 분산 모형을 표시하여 비교할 수 있으며, pdf을 예상하여 데이터 위로 표현해주는 함수이다.

#distplot의 파라미터 중에 수업 자료에서 사용한 부분만 설명하자면, a는 Series, list데이터를 받는 파라미터이며, kde값이 True이면 확률변수의 pdf선을 같이 보여주어 비교가능하게 해주는 파라미터이다. fit을 통해서는 샘플 데이터 위로 예측한 pdf를 그려줄 때 사용하는 파라미터이다.
```
