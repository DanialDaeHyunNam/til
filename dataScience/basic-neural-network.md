## Basic Neural Network

기저함수의 형태를 모수 값으로 변화시킬 수 있게하여 적응형 기저 함수 모형으로 이루어진 것을 신경망 모형이라 하며 구조적으로는 복수의 퍼셉트론을 쌓아놓은 형태 **MLP(Multi-Layer Perceptron)** 으로도 불린다.<br>

> 기저함수란 비선형 데이터를 분석할 때, 독립 변수를 그대로 사용하지않고 변환하는 함수를 의미한다.

퍼셉트론은
- 입력 x
- 가중치 w
- 바이어스 b
- 활성화 함수(Activation function) 입력값 a
  <br>
  **a = &Sigma;wx + b = w<sup>T</sup>x + b**
- 활성화 함수(Activation function) h와 출력값 z
  <br>
  **z = h(a) = h(w<sup>T</sup>x + b)**
- 최종 출력 y = z

##### 시그모이드 활성화 함수
일반적으로 활성화 함수 h는 시그모이드 함수 &sigma;를 사용한다. 그 중에서도 로지스틱 함수를 가장 많이 사용한다(미분을 쉽게 계산할 수 있으므로).<br>
**h(a) = &sigma;(a) = 1/1+e<sup>-&alpha;</sup>**
<br>
미분은 아래와 같이 쉽게 할 수 있다.<br>
**d&sigma;(a)/da = &sigma;(a)(1-&sigma;(a)) = &sigma;(a)&sigma;(-a)**
<br>
최종 클래스 값은
<br>
**y = sign(z - 1/2) = round(z)**
<br>
로 분류를 진행할 수 있다.

##### 하이퍼 패러미터에 의해 모양이 바뀌는 비선형 기저 함수
모수 &theta;를 사용하여 기저함수의 형태를 조절한다.
<br>
&phi;(x; &theta;)를 사용하면 &theta;값을 바꾸는 것으로 다양한 모양의 기저 함수를 시도할 수 있다.<br>
**z = h(w<sup>T</sup>&phi;(x; &theta;) + b)**

##### Universal Approximation Theorem
Universal Approximation Theorem에 따르면 적응형 기저함수를 충분히 많이 사용하면 어떠한 형태의 함수와도 유사한 형태의 함수를 만들 수 있다.

##### MLP(Multi-Layer Perceptrons)
구조는 Input layer -> Hidden layers -> Output layer로 이루어진다.
