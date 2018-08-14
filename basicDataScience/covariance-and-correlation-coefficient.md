## Covariance and correlation coefficient

두 개 이상의 서로 관련을 가지는 자료 값의 집합들이나 혹은 확률 변수들의 관계 즉 결합 분포는 Heatmap과 같은 서술 통계 방법으로 묘사하거나 결합 확률 분포를 사용하여 정의한다.<br>
다변수에도 평균과 분산과 같은 대표값이 존재하는데, 이가 **공분산과 상관계수** 이다.

- 샘플 공분산
**S<sub>xy</sub> = 1/N * &Sigma;(x<sub>i</sub> - m<sub>x</sub>)(y<sub>i</sub> - m<sub>y</sub>)**

즉 같은 부호를 가지는 경우에는 양의 방향으로 값이 커진다.

**샘플 상관계수** 는 <br>

**r<sub>xy</sub> = s<sub>xy</sub> / &radic;s<sub>x</sub><sup>2</sup> * &radic;s<sub>y</sub><sup>2</sup>**

- 확률변수의 공분산과 상관계수
**Cov[X, Y] = E[(X - E[X])(Y  - E[Y])]** <br>
**&rho;[X, Y] = Cov[X, Y] / &radic;Var[X] * &radic;Var[Y]**
<br>
**-1 <= &rho; <= 1**
  + &rho; = 1 : 완전선형 상관관계
  + &rho; = 0 : 무상관(독립과는 다름)
  + &rho; = -1 : 완전선형 반상관관계
<br>
- 다변수 확률 변수의 샘플 공분산
**&Sigma; = Cov[X] = E[(X - E[X])(X - E[X])<sup>T</sup>]**
