## Feedforward Propagation
신경망의 계산과정은 신호가 전달되는 과정과 비슷하여 순방향 전파(**Feedforward Propagation**)라고한다.<br>

l-1번째 계층의 출력과 l번째 계층의 출력은 다음과 같은 관계를 가진다.
a<sup>(l)</sup> = W<sup>(l)</sup>z<sup>(l-1)</sup> + b<sup>(l)</sup>
<br>
z<sup>(l)</sup> = h(a<sup>(l)</sup>)
<br>
가장 첫번째 레이어는 z<sup>(0)</sup> = x이며,
<br>
가장 마지막 레이어는 y = z<sup>(L)</sup>가 된다.
<br>
자세한 그림은 [링크](https://datascienceschool.net/view-notebook/0178802a219c4e6bb9b820b49bf57f91/)를 참고하자.

##### 오차 함수
오차함수는 조건부 확률이라는 실수 값을 출력해야 하므로 제곱합 오차 함수를 사용한다.

##### 최적화
Steepest gradient descent 방법을 적용하여 가중치를 갱신한다. &mu;는 step size이다.
<br>
**w<sub>k+1</sub> = w<sub>k</sub> - &mu;*(&part;C/&part;w)**
<br>
**b<sub>k+1</sub> = b<sub>k</sub> - &mu;*(&part;C/&part;b)**
<br>**C는 오차함수를 의미한다.**
<br>
