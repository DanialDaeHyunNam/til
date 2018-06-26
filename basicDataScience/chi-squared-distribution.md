## Chi-squared distribution

가우시안 정규 분포를 따르는 확률 변수 X의 n개의 샘플 x<sub>1</sub>, ... , x<sub>n</sub>을 제곱을 하여 더하면 양수값만을 가지는 분포가 된다. 이 분포를 카이 제곱 분포 **(Chi-squared distribution)** 라고 한다. 모수는 자유도(Degree of freedom)를 가진다.<br>
 **&Sigma;x<sub>i</sub><sup>2</sup> ~ &Chi;<sup>2</sup> (x; &nu;)** <br>
 카이 제곱 분포의 확률 밀도 함수는 다음과 같다.<br>
**&Chi;<sup>2</sup> (x; &nu;) = x<sup>(&nu;/2 - 1)</sup>e<sup>(-x/2)</sup> / 2<sup>&nu;/2</sup>&Gamma;(&nu;/2)** <br>
0에서 1사이를 뽑는 sp.stats.norm으로 확률변수를 설정하고, 나오는 샘플들을 제곱해서 더하게되면 직관적으로는 0에 점점 가까워지는 숫자가 가장 많이 나올 것이라는 느낌이 들지만, 실제로는 점점 mode값이 우측으로 변해가는 것을 확인할 수 있다. 이는 CLT에서 설명하듯 계속 겹쳐지면 결국 정규분포를 따라가는 것을 보여주는 사례이기도 하다.
