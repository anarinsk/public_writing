

**Understanding Regression**
 

2019-10-25

Jun Sok Huhh | :house:[lostineconomics.com](http://lostineconomics.com)

![](https://i.stack.imgur.com/rDYMh.png =500x)

여기서 회귀분석을 해설할 생각은 없다. 이미 너무나 많은 그리고 매우 훌륭한 내용들이 책, 웹, 강의로 넘쳐날테니까. 이 글의 용도는 그림 하나로 지나치게 쉬운 회귀분석의 '핵심'을 살피는 것이다. [crossvalidated](https://stats.stackexchange.com/questions/123651/geometric-interpretation-of-multiple-correlation-coefficient-r-and-coefficient)에서 이 그림을 보는 순간 일종의 '돈오돈수'가 강림했다. (이렇게 이해하면 쉬웠을 것을...) 먼저 우리에게 익숙한 회귀분석 모델을 매트릭스로 적어보자. 

$$
\underset{n \times 1}{\phantom{\bm \gamma}\mathbf{Y}\phantom{\bm \gamma}} = \underset{n \times k}{\phantom{\bm \gamma} \mathbf{X} \phantom{\bm \gamma} }\underset{k \times 1}{\bm \beta} + \underset{n \times 1}{\phantom{\bm \beta} \bm \varepsilon \phantom{\bm \gamma} }
$$

식에 관한 자세한 설명 역시 생략한다. 대충 $n$ 개의 관찰 수과 $k$ 개의 regressor를 지닌 중회귀분석 모형이라고 생각하면 되겠다.  앞서 본 그림은 보통 회귀분석의 예시로 많이 활용되는 아래 그림과는 다르다.[^1]

[^1]: 흔히 $\mathbf Y$를 종속변수, $\mathbf X$를 독립변수로 부르기도 한다. 하지만 이러한 이름에는 혼란의 여지가 있다. 여기서는 regressor, regressand라는 영어 표현을 그대로 쓰도록 하겠다. 

![](https://miro.medium.com/max/1720/1*G1Y_-X14q2xMVHlUuaUUdA.png =500x)

위 그림은 1개의 regressor가 존재할 때 이것과 regressand를 그대로 2차원 평면에 관찰 수만큼 찍은 것이다. 첫번째 그림에서 "Observed Y"는 $n$ 개의 regressand를 모두 포괄한다. $\mathbf{Y}$는 $(n \times 1)$ 벡터, 즉 $n$ 차원 벡터다. 이 벡터 하나가 식 관찰값 전체를 나타낸다. 

regressor $\mathbf X$가 표현할 수 있는 공간의 최대 차원, 즉 $\mathbf X$의 랭크는 무엇일까? 회귀분석에서는 대체로 $n > k$가 일반적이고 이런 상황에서 $\mathbf X$의 랭크는 $k$를 넘을 수 없다. 다시 말하면, $\mathbf X$가 생성하는(span)하는 컬럼 스페이스(앞으로 col $\mathbf X$로 표기하자)의 차원은 $k$를 넘을 수 없다. 

그림에서 색칠된 평면이 $\mathbf X$가 생성하는 컬럼 스페이스, 즉 col $\mathbf X$를 표현하고 있다. 앞서 보았듯이 $\mathbf Y$는 $n$ 차원 벡터다. 특별한 경우가 아니라면 $\mathbf Y$ 벡터가 col $\mathbf X$에 속할 가능성은 거의 없다. 만일 속해 있다면 회귀분석이 필요 없을 것이다. col $\mathbf X$를 통해서 $\mathbf Y$를 완벽하게 예측할 수 있는데, $\mathbf Y$와 col $\mathbf X$의 거리를 왜 최소화해야 할까. 

회귀분석의 목표는 regressor를 통해서 regressand를 '가장' 잘 설명하는 것이다.[^1] 이를 기하적으로 풀어보자. 회귀분석이란 regressand와 닮은 어떤 것을 col $\mathbf X$에서 찾는 것이다. 즉 $\mathbf Y$와 닮은 무엇을 $\mathbf X$의 컬럼 스페이스에 찾아야 한다. 직관적으로 쉽게 떠올릴 수 있는 것은 이 평면과 $\mathbf Y$의 (유클리드) 거리를 가장 짧게 만들어주는 벡터일 것이다. 그리고 이 최단거리는 $\mathbf Y$에서 $\mathbf X$ 컬럼 스페이스로 내린 수선의 발이 닿는 col $\mathbf X$의 지점이다. 이 위치를 구해주는 연산자(operator)가 회귀분석 계수 $\hat{\bm \beta}$이다. 즉, 

$$
\hat{\bm \beta} = ({\mathbf X}'{\mathbf X})^{-1} ({\mathbf X}' \mathbf Y)
$$

그리고 이 연산자를 regressor의  모음인 col $\mathbf X$에 적용하면 regressand $\mathbf Y$의 예측치 $\hat{\mathbf Y}$이 계산된다. 그림에서 보듯이 $\hat{\mathbf Y}$은 $\mathbf Y$와 $\mathbf X$의 컬럼 스페이스의 거리를 최소화하는 위치에 존재한다. 

이제 이 그림을 머리에 넣고서 $\mathrm R^2$의 의미를 살펴보자. 결론부터 이야기하면  $\mathrm R^2$는 그림에서 $(\mathbf Y - \overline{\mathbf Y})$ 벡터와 $(\hat{\mathbf Y}-\overline{\mathbf Y})$ 벡터가 이루는 각의 코사인 값, 즉 $\cos \theta$다. $\overline{\mathbf Y}$는 무엇일까? 그림에서처럼 $\overline{Y} \mathbf{1}_n$로 표기할 수 있다. 즉, $\mathbf Y$의 평균값 $\overline{Y}$만으로 구성된 $(n \times 1)$ 벡터다. 이 벡터는 col $\mathbf X$ 안에 있을까? 당연히 그렇다. $\mathbf X$는 최대한 $k(<n)$ 차원의 벡터이고, $\overline{\mathbf Y}$는 1차원 벡터다. 다시 본론으로 돌아가자. 이 코사인 값의 의미는 무엇일까? 

그림에서 보듯이 세 개의 벡터가 직각삼각형을 이루고 있으므로 아래의 식이 성립한다. 

$$
\underset{\text{TSS}}{\Vert \mathbf Y - \overline{\mathbf Y} \Vert^2} = \underset{\text{RSS}}{\Vert \mathbf Y - \hat{\mathbf Y} \Vert^2} + \underset{\text{ESS}}{\Vert \hat{\mathbf Y} - \overline{\mathbf Y} \Vert^2}
$$

흔한 피타고라스의 정리다. 그런데 이것 어디서 많이 보던 식이다. 회귀분석 배우면 언제나 나오는 식이다. Regressand의 평균과 관찰의 이른바 총 제곱의 합(TSS: Total Sum of Squares)은 설명된 제곱의 합(ESS: Explained Sum of Squares)과 잔차 제곱의 합(RSS:Residual Sum of Squares)와 같다. 대체로 복잡하게 소개되는 이 식이 기하학적으로 보면 그냥 피타고라스의 공식에 불과한 것이다.  

양변을 $\Vert \mathbf Y - \overline{\mathbf Y} \Vert^2$으로 나누면 다음과 같다. 

$$
1 =  \dfrac{\Vert \mathbf Y - \hat{\mathbf Y} \Vert^2}{\Vert \mathbf Y - \overline{\mathbf Y} \Vert^2} + \dfrac{\Vert \hat{\mathbf Y} - \overline{\mathbf Y} \Vert^2}{\Vert \mathbf Y - \overline{\mathbf Y} \Vert^2}
$$

정의에 따라서 $1 = \dfrac{\text{RSS}} {\text{TSS}} +  {\mathrm R}^2$가 된다. 

$\textrm R^2$는 가끔 회귀분석의 성과 지표로 남용되는 경우가 있다. 그런데 이렇게 기하학적으로 보면 col $\mathbf X$ 내에 표현된 $\hat{\mathbf Y}$ 가 $\mathbf Y$와 얼마나 가깝게 있는지를 지표화한 방식의 하나에 불과하다. 

Jun Sok Huhh | :house:[lostineconomics.com](http://lostineconomics.com)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYxOTMwNjM4LC0xOTYyOTM5MzU1LC0xNT
EzODIwMzE5XX0=
-->