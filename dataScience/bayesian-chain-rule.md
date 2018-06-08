## Bayesian chain rule

직관적으로 해석하는 것에 힘든 시간을 보냈다.
이 [링크](https://math.stackexchange.com/questions/2187509/applying-the-chain-rule-probability-with-three-variables)에서 나온 설명을 통해서 이해를 할 수 있었는데, 핵심적으로 이해해야했던 점은 P(A, B, C)/P(A) = P(B, C | A)라는 점이었다.

 그 특성을 이용하면
 **P(A, B, C) = P(C | B, A) * P(B | A) * P(A)**
 에서
 **P(A, B, C)/P(A) = P(C | B, A) * P(B | A)**
 즉,
 **P(B, C | A) = P(C | B, A) * P(B | A)** 를 얻을 수 있다.

 수업시간에 박사님이 출제하신 문제의 경우는 4개의 변수가 있는 식으로,
 **P(A, B | C, D) = P(B, C | A, D) * P(A | D) / P(C | D)**
 
