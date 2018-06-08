## Bayesian chain rule

직관적으로 해석하는 것에 힘든 시간을 보냈다.
이 [링크](https://math.stackexchange.com/questions/2187509/applying-the-chain-rule-probability-with-three-variables)에서 나온 설명을 통해서 이해를 할 수 있었는데, 핵심적으로 이해해야했던 점은 **P(A, B, C)/P(A) = P(B, C | A)** 라는 점이었다.

 그 특성을 이용하면<br>
 **P(A, B, C) = P(C | B, A) * P(B | A) * P(A)**<br>
 에서<br>
 **P(A, B, C)/P(A) = P(C | B, A) * P(B | A)**<br>
 즉,<br>
 **P(B, C | A) = P(C | B, A) * P(B | A)** 를 얻을 수 있다.<br>

 수업시간에 박사님이 출제하신 문제의 경우는 4개의 변수가 있는 식으로,<br>
 **P(A, B | C, D) = P(B, C | A, D) * P(A | D) / P(C | D)**<br>

 한글로 된 좋은 자료로는 [여기](http://wolfpack.hnu.ac.kr/2015_Fall/D4BE/DBE_확률.pdf)를 발견하였고 여기서는 예제 등을 통해서 이해를 도울 수 있다.
