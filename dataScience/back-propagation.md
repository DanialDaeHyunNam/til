## Back Propagation
역전파(**Back Propagation**)을 수식으로 표현하면 다음과 같다.
<br>
**&delta;<sub>j</sub><sup>(l)</sup> = &part;C/&part;a<sub>j</sub><sup>(l)</sup>**
<br>
**&delta;<sub>j</sub><sup>(l-1)</sup> = h<sup>'</sup>(a<sub>j</sub><sup>(l-1)</sup>)&Sigma;w<sub>ij</sub><sup>(l)</sup>&delta;<sub>j</sub><sup>(l)</sup>**
<br>
Cost 함수가 C = 1/2(y - z)<sup>2</sup>이라면 최종단의 &delta;는 예측 오차 그 자체이다.
<br>
&delta;<sub>j</sub><sup>(l)</sup> = y<sub>j</sub> - z<sub>j</sub>
<br>
따라서 역전파를 오차 역전파(**Error Back Propagation**)이라고 한다.
