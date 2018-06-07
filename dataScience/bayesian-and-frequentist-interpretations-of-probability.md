## Bayesian and frequentist Interpretations of Probability


> 아래는 위키백과에서 가져온 내용이다

##### 발생빈도주의

고전적 확률이론에서는 모든 가능성을 지닌 경우의 수에 대한 원하는 경우의 수의 비이다. 쉬운 예로 6면체 주사위에서 2의 배수가 나올 확률은 ½이고, 3의 배수가 나올 확률은 ⅓이다.

##### 베이즈 확률론

확률론과 통계학에서, 베이즈 정리(Bayes’ theorem)는 두 확률 변수의 사전 확률과 사후 확률 사이의 관계를 나타내는 정리다. 베이즈 확률론 해석에 따르면 베이즈 정리는 사전확률로부터 사후확률을 구할 수 있다.

베이즈 정리는 불확실성 하에서 의사결정문제를 수학적으로 다룰 때 중요하게 이용된다. 특히, 정보와 같이 눈에 보이지 않는 무형자산이 지닌 가치를 계산할 때 유용하게 사용된다. 전통적인 확률이 연역적 추론에 기반을 두고 있다면 베이즈 정리는 확률임에도 귀납적, 경험적인 추론을 사용한다.

> 개인적인 생각

현재 듣고있는 수업에서 베이즈 정리는 확률이라는 표현보다는 해당 주장에 대한 신뢰도라고 설명했다. 그때는 그 의미를 정확히 이해할 수 없었지만, 여러 자료들을 살펴보면서 의미를 조금 이해할 수 있었다. 우리가 어려서부터 배우는 지식이 우리가 이해해가는 과정이 베이즈 정리에서 설명하고자하는 바와 아주 흡사하다는 생각에 앞으로 다가올 공부 내용에 상당한 동기부여가 된다. 데이터 사이언스를 공부하며 좀 더 실제 예를 들어가며 후에 다시 관련 내용들을 작성하겠다.

### 베이즈 정리 기본 공식

$$ P(A|B) = \dfrac{P(B|A)P(A)}{P(B)} $$

### 베이즈 정리의 확장

만약 사건 $A_i$가 다음의 조건을 만족하는 경우,

* 서로 교집합이 없고

<p align="center">
<img src="https://latex.codecogs.com/svg.latex?\Large&space;A_i \cap A_j = \emptyset" title="\Large A_i \cap A_j = \emptyset" />
</p>

* 모두 합쳤을 때 (합집합) 전체 표본 공간이면

<p align="center">
<img src="https://latex.codecogs.com/svg.latex?\Large&space;A_1 \cup A_2 \cup \cdots = \Omega" title="A_1 \cup A_2 \cup \cdots = \Omega" />
</p>


전체 확률의 법칙을 이용하여 다음과 같이 베이즈 정리를 확장할 수 있다.

<p align="center">
<img src="https://latex.codecogs.com/svg.latex?\Large&space;P(A_1|B) = \dfrac{P(B|A_1)P(A_1)}{P(B)} = \dfrac{P(B|A_1)P(A_1)}{\sum_i P(A_i, B)}= \dfrac{P(B|A_1)P(A_1)}{\sum_i P(B|A_i)P(A_i)}" title="\Large P(A_1|B) = \dfrac{P(B|A_1)P(A_1)}{P(B)} = \dfrac{P(B|A_1)P(A_1)}{\sum_i P(A_i, B)}= \dfrac{P(B|A_1)P(A_1)}{\sum_i P(B|A_i)P(A_i)}" />
</p>


<a href="http://www.codecogs.com" target="_blank"><img src="http://www.codecogs.com/images/poweredbycodecogs.png" border="0" title="CodeCogs - An Open Source Scientific Library" alt="CodeCogs - An Open Source Scientific Library"></a>
