**Math Behind PCA**

2019-05-17
Jun Sok Huhh | :house:[lostineconomics.com](http://lostineconomics.com)

# Synopsis 

* PCA는 무엇을 최적화하는 것일까? 
* PCA에서 왜 아이겐밸류와 아이겐벡터가 중요할까? 

# PCA 

"차원의 저주"라는 표현이 있다. 언뜻 보면 자명한 이야기 같지만, 곰곰이 생각해보면 모호한 구석이 많다. 관찰 수는 많을수록 좋은데 차원은 관찰과 어떻게 다를까? 쉽게 생각해보자. 관찰 수란 활용할 수 있는 샘플의 수다. 이는 당연히 많을수록 좋다. (물론 미칠 듯이 많으면 새로운 문제가 발생하긴 하나, 대체로 우리는 샘플이 부족해서 문제를 겪는다) 하나의 샘플에서 관찰 가능한 변수가 7개라고 해보자. 샘플 수에 따라서는 적당해 보일 수 있다. 그런데, 샘플은 100 개인데, 한 샘플에서 관찰할 수 있는 포인트가 1,000 개라고 치자. 이 데이터 셋은 10만 개의 개별 포인트를 지닌 제법 큰 데이터 셋이지만 별 쓸모는 없다. 관찰 수에 비해서 개체의 차원이 지나치게 크기 때문이다. 이럴 경우 어떻게 차원을 줄이면 좋을까? 쉽게 생각할 수 있는 방법은 1,000 개의 특징들을 좀 줄여보는 것이다. 주성분분석(Principal Component Analysis)는 이를 위해 필요한 방법이다.

# 원래 하고 싶은 게 뭔데? 

대체로 많은 PCA에 관한 설명들이 원래 하고 싶은 게 무엇인지에 관해 묻지 않는다. PCA란 데이터의 특성을 압축하는 방법이라는 이야기만 할 뿐. 수학적으로 말하면 목적함수에 관한 질문이고 우리는 먼저 이 질문에 집중하겠다. 

대체로 통계학의 알고리듬은 목적 함수를 최적화하는 형태이다. PCA도 마찬가지다. $i$ 관찰 대상에 관한 $k$ 차원의 피처 벡터 $x^i$가 있다고 하자. 즉, $x^i$는 $k \times 1$의 칼럼 벡터이다. 앞으로 특별한 언급이 없는 이상 앞으로 $x_i$ 벡터는 $n$개의 관찰에 대한 평균으로 구성된 벡터 $\mu = [\mu_1~\mu_2~\dotsc~\mu_k]^T$를 뺀 값이라고 간주하자. 즉, $X^i$가 평균을 빼지 않은 $i$ 관찰 대상이라고 할 때, 

$$
x^i = \left[\begin{array}{c}{X^i_{1} - \mu_1} \\ {X^i_{2} - \mu_2} \\ {\vdots} \\ {X^i_{k} - \mu_k}\end{array}\right]
$$ 

이제 해당 피쳐를 쏠 스크린으로 활용할 유닛 벡터를 $w$라고 하자. 유닛 벡터란 $w \cdot w = 1$를 의미한다. 여기서 스크린이라는 의미는 개별 관찰이 지니는 특징을 벡터로 투영해서 그 특징을 요약하겠다는 것이다. 우리에게 익숙한 회귀분석 역시 $y_i$라는 관찰을 $\mathbf X$라는 설명변수로 프로젝션해서 계수를 구하는 방법이다. 좌우간, $x^i$를 $w$로 프로젝션 하면 다음과 같다.

$$
\operatorname{Proj}_{w}(x_i) = \dfrac{w \cdot x^i}{\Vert w \Vert} = w \cdot x^i
$$

이 프로젝션의 벡터 공간 $w$에서의 좌표는 $(w \cdot x^i) w$가 된다. 그리고 이 프로젝션 스칼라 값 혹은 프로젝션 벡터의  기댓값은  아래와 같이 0이 된다. 물론 벡터의 경우에는 스칼라 대신 $k \times 1$의 0 벡터가 된다. 

$$
\dfrac{1}{n} \sum^n_{i=1} (w \cdot x^i) = \left( \dfrac{1}{n} \sum_{i=1}^n x^i \right)\cdot w = 0 \cdot w
$$

원 자료 즉, 벡터 $x_i$와 이 프로젝션 좌표의의 유클리드 거리를 구해보자. 

$$
\begin{aligned}
\Vert x^i - (w \cdot x^i) w \Vert^2 & = \Vert x^i \Vert^2 - 2 (w \cdot x^i)(w \cdot x^i) +  \Vert w \Vert^2 \\
& = \Vert x^i \Vert^2 - 2 (w \cdot x^i)^2 +  1
\end{aligned}
$$

모든 관찰 수 $n$에 대해서 거리를 구해 더하면 이것이 RSS (Residual Sum of Squares)가 된다.  

$$
\begin{aligned}
\mathrm{RSS}(w) & = \sum_{i=1}^n \left( \Vert x^i \Vert^2 - 2(w \cdot x^i)^2 + 1 \right)  \\
& = \left(  n +  \sum_{i=1}^n \Vert x^i \Vert^2 \right) - 2 \sum_{i=1}^n  (w \cdot x^i)^2
\end{aligned}
$$

RSS를 최소화하는 게 목표라고 하자. 조정 가능한 값인 $w$는 괄호를 제외한 부분에만 포함되어 있다. 이를 아래와 같이 고쳐써보자. 

$$
\dfrac{1}{n} \sum_{i=1}^n (w \cdot x^i)^2 = \left(\dfrac{1}{n}  \sum_{i=1}^n w \cdot x^i \right)^2 + \mathrm{Var}[w \cdot x^i]
$$

이 식이 성립하는 이유는 $\mathrm{Var}(x) = \mathrm{E}(x^2) - (\mathrm{E}(x))^2$이 성립하기 때문이다.  그리고 앞에서 보았듯이 $E(w \cdot x^i) = 0$ 성립한다. 따라서 RSS를 최소화한다는 것은 $\mathrm{Var}(\cdot)$을 최대화하는 것과 같다. 

여기서 잠깐. 하나의 벡터로만 프로젝션하라는 법은 없다. 프로젝션의 스크린으로 동원되는 벡터가 $w_1, w_2, \dotsc, w_k$라고 하자. 이 프로젝션을 통해 생성되는 벡터 공간은 다음과 같이 나타낼 수 있다. 

$$
\sum_{i=1}^k \underset{\mathrm{가중치}}{( x^i \cdot w_i) } w_i
$$

이 녀석의 RSS를 최소화하는 문제는 어떻게 될까? 만일 $w_\cdot$들이 서로 직교한다면, 벡터들의 크로스 프로덕트들은 0이 되어 사라질 것이다.  결국 스크린을 이루는 축들과 $x^i$의 크로스 프로덕트 값의 분산을 더한 값을 최대화하는 것이 RSS를 극소화 문제가 된다. 

아래 그림이 PCA를 이해하는 데 다소 도움이 될 수 있겠다. OLS는 모델의 직선과 관찰의 유클리드 거리를 극소화하는 것이다. 반면 PCA는 특정한 벡터를 두고 이 벡터로 개별 관찰 벡터를 프로젝션 했을 때, 그 프로젝션된 이미지 벡터와 관찰 간의 거리를 최소화하는 것이다. 프로젝션이 직교하게 선을 내리는 것이라는 점을 떠올리면 아래 그림의 오른쪽이 쉽게 이해가 갈 것이다. 

![Image result for PCA regression](https://i.stack.imgur.com/83Jog.png)

# 분산-공분산 행렬 

이제 왜 분산이 등장하는지는 대충 이해가 될 것이라고 생각한다.  $X$를 통해 쉽게 분산-공분산 행렬을 나타낼 수 있다. $x_i^j$ 에서 $i (=1,2,\dotsc, n)$는 관찰을, $j(=1,2,\dotsc,k)$는 피쳐를 나타낸다. 

$$ 
\underset{n \times k}{X} = 
 \left( \begin{array}{ccc}{
{{x^1}^T}}  \\ \\
{{x^2}^T} \\ \\
{\vdots} \\ \\
{{x^n}^T} \end{array}\right) = 
\left( \begin{array}{ccc}
{x_1^1} & {x_2^1} & {\cdots} & {x_k^1} \\ 
{x_1^2} & {x_2^2} & {\cdots} & {x_k^2} \\ 
{\vdots} & {\vdots} & {\ddots} & {\vdots} \\ 
{x_1^n} & {x_2^n} & {\cdots} & {x_k^n} 
\end{array}\right) 
$$

$$
\begin{aligned}
\dfrac{1}{n-1} \underset{k \times k}{X^{T} X}
=  \left( \begin{array}{ccc}{
\operatorname{cov}\left(x_{1}, x_{1}\right)} & {\operatorname{cov}\left(x_{1}, x_{2}\right)} & {\cdots} & {\operatorname{cov}\left(x_{1}, x_{k}\right)} \\ 
{\operatorname{cov}\left(x_{2}, x_{1}\right)} & {\operatorname{cov}\left(x_{2}, x_{2}\right)} & {\cdots} & {\operatorname{cov}\left(x_{2}, x_{k}\right)} \\ 
{\vdots} & {\vdots} & {\ddots} & {\vdots} \\ 
{\operatorname{cov}\left(x_{k}, x_{1}\right)} & {\operatorname{cov}\left(x_{k}, x_{2}\right)} & {\cdots} & {\operatorname{cov}\left(x_{k}, x_{k}\right)}\end{array}\right) = \Sigma
\end{aligned}
$$

# 아이겐밸류는 어떻게 등장하나? 

임의의 단위 벡터 $w$와 그 프로젝션을 다시 적어보자. 이제 하나의 벡터가 아니라 $X$라는 매트릭스 전체에 대해서 프로젝션을 하면 아래와 같다.

$$\operatorname{Proj}_{w} (X) = \dfrac{X w}{\Vert w \Vert} \in {\mathbb R}^{n \times 1}$$

이제 극대화의 목적은 이렇게 프로젝션된 이미지의 분산을 가장 크게 만드는 것이다. 
$$
\begin{aligned}
\mathrm{Var}(X {w})=\frac{1}{n-1} \sum_{i=1}^{n} \left( X {w} - \mathrm{E}(Xw) \right)^{2}=\frac{1}{n-1} \sum_{i=1}^{n}(X {w})^{2}
\end{aligned}
$$

앞서의 가정에 따라서 $\mathrm{E}(X) = 0$가 성립함을 기억해두자. 

$$
\begin{aligned}
\mathrm{Var}(X {w}) &= \frac{1}{n-1}(X {w})^{T}(X {w}) \\
&=\frac{1}{n-1} {w}^{T} X^{T} X {w} =\frac{1}{n-1} {w}^{T}\left(X^{T} X\right) {w} \\
&={w}^{T}\left(\frac{X^{T} X}{n-1}\right) {w} \\
&={w}^{T} \Sigma {w}
\end{aligned}
$$

그런데, $w$는 단위벡터임으로 $w \cdot w = 1$이다. 이를 제약 조건으로 두고 제약 하의 극대화 문제를 정식화하면 다음과 같다. 

$$
\begin{aligned}
{\mathcal L} =w^{\operatorname T} \Sigma w - \lambda (w \cdot w -1) 
\end{aligned}
$$

$$
\begin{aligned}
\dfrac{\partial \mathcal L}{\partial w} & = 0 = 2 \Sigma w - 2\lambda w \\
\dfrac{\partial \mathcal L}{\partial \lambda} & = 0 = w \cdot w - 1
\end{aligned}
$$

1계 조건에 따르면, $\Sigma w = \lambda w$가 성립해야 한다. 사실 이 조건은 상당히 신기하다. 1계 조건이 정확하게 아이겐밸류와 아이겐벡터를 구하는 방법과 동일하다. 어떤 매트릭스가 있을 때 해당 매트릭스의 분산-공분산 행렬의 아이겐밸류와 아이겐벡터를 구하면 그 아이겐밸류와 벡터가 바로 RSS를 최적화해주는 값이 된다. 이때 $w$는 아이겐벡터이며 $\lambda$는 아이겐밸류가 된다.  게다가 아이겐밸류는 아래 식에서 보듯이 그 자체로 분산과 같다. 

$$
\operatorname{Var}(X w) = w^{\mathrm T} \Sigma w =  \lambda w \cdot w = \lambda$$ 

해당 아이겐벡터는 RSS를 최소화시켜주는 스크린의 벡터, 즉 좌표가 된다. 이는 $k \times 1$ 값을 지니게 될텐데 $k$ 개의 피쳐를 RSS를 최소화하는 방식으로 이 스크린 위에 투영시킬 때 각 피쳐가 어느 방향으로 움직여야 하는지에 관한 정보를 담고 있다. 앞서 피쳐를 여러 개의 스크린으로 프로젝션한다는 이야기를 했다. 즉 아이겐벡터가 $k$ 개라고 하면, 투영할 수 있는 스크린이 $k$ 개라는 뜻이기도 하다. 

$\lambda$가 분산이 된다고 말했다. 잠깐, 분산이라면 항상 0보다 커야 하는데, $\lambda$가 0보다 크다는 보장이 있는가? 이 문제를 포함하여 앞에서 정리하지 못한 몇 가지 문제를 모아서 살펴보자. 

# 분산-공분산 행렬의 속성 

## 대칭 행렬
$\Sigma$는 행렬로서 두 가지 특징을 만족한다. 우선, 분산-공분산 행렬이므로 대칭적이다. 행렬이 대칭일 경우 해당 행렬의 아이겐벡터들은 서로 직교한다. 

$$
i, j \in \{ 1, 2, \dotsc, k\}~\text{with}~i \ne j, w_i \cdot w_j = 0
$$ 

여러개의 프로젝션 스크린 벡터들이 존재할 경우 해당 벡터들이 서로 직교하면 분산값의 합을 최대화하는 것과 RSS를 최소화하는 것이 같음을 보았다. 이 조건이 분산-공분산 행렬의 속성을 통해 성립한다. 

## Positive-definite 

$\Sigma$는 양정행렬이다. 

$$
x^T \Sigma x > 0 ~\text{for any $x$.}
$$

이 경우 모든 아이겐밸류의 값은 음수가 될지 않는다. 앞서 아이겐밸류가 분산이 된다고 것을 보았는데, 아이겐밸류가 음수가 될 수 없고 따라서 분산이라는 결과에 부합한다. 

이 두 조건에 따라서 개별 프로젝션 스크린 벡터에 따른 극대화 문제를 풀면 아이겐밸류와 아이겐벡터를 각각 하나씩 얻게 된다. 분산이 큰 순서대로 아이겐벡터를 정렬한다고 생각해보자. 이렇게 정렬하면 프로젝션 스크린 벡터 중에서 RSS를 더 줄일 수 있는 벡터 순으로 정렬하는 셈이다.  

# 차원 축소 

이제 마지막으로 차원 축소가 나온다. 만일 $k$ 개의 차원에서 의미 있는 차원이 $l (< k)$ 개에 불과했다면 앞서의 식을 통해서 $l$ 개의 아이겐밸류-아이겐벡터를 얻고 나머지 아이겐밸류는 0이 될 것이다. 이 경우 우리는 $l$ 개로 축소된 차원을 얻게 된다.

하지만 현실적으로 $(k-l)$ 개의 아이겐밸류가 0이 되는 경우는 드물다. 이때 0으로 간주한 아이겐밸류에 대한 기준값을 잡거나 혹은 임의로 가장 설명력이 큰 $l$ 개의 프로젝션 스크린 벡터를 취하는 것을 약속할 수 있겠다. 설명력이 크다는 것은 무엇일까? 분산이 크다는 것이다. 앞서 보았듯이 여러 개의 프로젝션 벡터가 있을 때 해당 분산값이 합이 큰 것이 좋다. 따라서 $l$ 개를 취할 때에는 분산이 큰 순서대로 취하면 된다. 

# Resource 

이 글은 아래 자료를 바탕으로 만들었습니다. 

https://www.stat.cmu.edu/~cshalizi/350/lectures/10/lecture-10.pdf


:feet:Jun Sok Huhh | :house:[lostineonomics.com](http://lostineconomics.com)




<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMwNjA4Mjc3OSw2ODk0MTA3LDIwMTE1Mz
QxODUsLTQ0ODExMjMxMiwtMTQ5ODQyNDMwMCwtMTc1NDE3OTUw
OCwtMTc1OTYzNTA5NCw3MTM5ODM1MDQsLTE5OTE0NzM1NzEsMT
AyMzM2NTQ5Nyw4OTM3NjI5MDAsLTkzMzM1NTMxOSw4NjExODky
ODIsMTI4MzAzOTkzNSwtMTk4NDE4Nzc1OV19
-->