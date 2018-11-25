**Claude Shannon's Entropy**

2018-11-22
Jun Sok Huhh | :house:[lostineconomics.com](http://lostineconomics.com)

# 엔트로피? 

나의 문송한 상식으로 엔트로피는 '무질서도' 쯤 된다. 열역학의 개념 말이다. 그런데 기계학습에서 이 녀석이 왜 나오지? 결론부터 말하면 내가 몹시도 과문 했다. 사실 이 둘 사이에 내밀한 연관 관계가 존재했다. 이는 제임스 글릭이 쓴 [인포메이션](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=56868821) 9장에 자세하게 소개되어 있고 참고하시면 되겠다. 간략하게 마음대로 요약해 보자. 

이른바 열역학 제2법칙으로 알려진 내용에서 "엔트로피의 증가"는 통계적인 경향성이다. 즉 경향적으로 증가한다. 그렇다면 이 경향성을 파악할 수만 있다면 엔트로피의 증가를 막는 영구 운동이 가능하지 않겠는가! 이러한 경향성을 미리 알 수 있는 이른바 맥스웰의 도깨비라는 유비가 이런 발상을 낳았다. 이것이 "영구기관"이라는 미몽의 이론적 시작이기도 하다고. 

좋다. 그런 도깨비가 있다고 치자. 이 도깨비는 어떻게 관련 정보를 얻게 되는가? 도깨비라면 0에 가까운 비용으로 이런 정보를 얻을 수 있겠지 그런 도깨비는 실존하지 않는다. 물질의 상태에 관한 정보를 얻기 위해서는 그에 상응하는 댓가를 치러야 한다. 도깨비가 정보를 알게 되면 알게 될수록 엔트로피는 높아진다. 

섀넌이 착목한 지점이 바로 이것이었다. 어떤 정보의 상태가 불확실하다고 할 때, 이 불확실성을 파악하기 위해서는 더 많은 정보가 필요하다. 만일 상태가 불확실하지 않다면 정보가 덜 필요할 것이다. 이점에서 어떤 시그널, 즉 정보의 상태 혹은 품질을 파악하는 측정치로 엔트로피를 쓸 수 있지 않을까? 잡음은 적고 시그널은 많은 정보일수록 엔트로피는 낮을 터다. 밑천이 드러나기 전에 여기까지만. 

# 엔트로피를 정의하기 위한 요소 

## 의외성(surprisal) 
제임스 글릭의 책에서 surpirsal을 "의외성"으로 번역했으므로 우리도 따르도록 하자. 의외성이란 어떤 사건이 주는 놀라움의 정도다. 월드컵 축구에서 한국이 독일을 이길 확률은 높지 않다. 이런 사건이 발생했다면 이는 의외성의 수준이 높은 사건이다. 유한한 전체 사건의 인덱스를 $1, \dotsc, n$이라고 하자. 이때 사건 $i$가 발생할 확률을 $p_i$라고 하자. 이때 이런 $p_i$가 지니는 의외성 $s$를 다음과 같이 정의하자. 

$$
s = -\log p_i
$$

$p_i$가 낮을수록 높을 값을 지니게 되기 때문에 앞에 마이너스를 붙였다고 생각해도 좋다. 아니면, $p_i$가 0과 1사이의 값이기 때문에 log의 값이 마이너스가 되고 여기에 다시 마이너스를 붙여주면 플러스 값이 된다. 

## Entropy
우리가 수량화하고 픈 것은 개별 사건이 아니라 현재의 불확실한 상태 전반이다. 앞서 정의한 개별 사건의 의외성을 뭔가 전체를 대표하는 값으로 바꿔야 한다. 기대값을 구하면 된다. 앞서 정의한 $s$가 확률변수이기 때문에 기대값 역시 다음과 같이 쉽게 정의할 수 있다. 이 기대값이 바로 정보의 엔트로피다. 

$$
e = - \sum_{i=0}^{n} p_i \log p_i
$$

## Cross entropy 
섀넌이 정의한 크로스 엔트로피는 다음과 같다. 동일한 배후 사건들에 관해서 두 개의 확률 분포를 $p$, $q$라고 하자. 이때 $p$를 사건의 참 확률분포라고 하고 $q$를 이에 대한 추정치라고 하자. $p$, $q$가 이산 확률분포라면 교차 엔트로피는 다음과 같이 정의한다. 

$$
H(p, q) = -\sum_{i=0}^n p_i \log q_i
$$

$q$는 $p$의 추정이므로 직관적으로 $H(p,q) \geq H(p,p) = e$.  이를 눈으로 확인해보고 싶다면 [LINK](https://www.desmos.com/calculator/zytm2sf56e)를 참고하시라. 

교차 엔트로피의 의미는 무엇일까? Kraft-McMillan 정리에 따르면, 교차 엔트로피는 참인 분포가 $p$이고 이에 관한 불완전한 추정 분포 $q$가 있을 때, 개별 실현값을 맞추기 위해 필요한 질문 수의 기대값이 된다. 즉,$p_x$에 대한 추정치 $q_x$로 참인 $p_x$를 맞출 때까지 소모되는 정보의 크기다. 쉽게 비유를 하자면 스무고개을 생각하면 되겠다. 예/아니오로 구별되는 이진 분류의 교차 엔트로피를 예로 적어보자. 

 $$
 \begin{aligned}
 H(p,q) = & - \sum_{i=0}^1 p_i \log (q_i) \\
 = & -( p_0 \log q_0 + p_1 \log q_1 ) \\
 = & -\left( p_0 \log q_0 + (1-p_0) \log (1-q_0 ) \right) 
 \end{aligned}
 $$

# Decision tree에서 어떻게 활용되는가? 

앞서 보았듯이 섀넌이 가져다 쓴 엔트로피는 일종의 정보에 관힌 품질 지표로 활용될 수 있다. 이른바 의사결정 나무(decision tree)란 판단을 해야 하는 어떤 분기에서 어떤 기준으로 데이터를 나누는 것을 의미한다. 무엇을 기준으로 결정 나무의 가지를 나눌까? 나무의 결정 노드를 가르는 기준으로 엔트로피를 활용하면 좋지 않을까? 정보 엔트로피를 기준으로 삼은 결정 노드의 판별 기준을 정보 이득(information gain)이라고 하고 그 정의는 아래와 같다. 

$$
IG(S, A(v)) = e(S) - \sum_{v \in A(v)} \dfrac{|S_v|}{|S|} e(S_v) 
$$

- $S$: all of events
- $A(v)$ a set of an attribute where element is denoted by $v$. 
- $e(X)$: entropy for the event set $X$

즉, 현재 아무런 feature도 활용하지 않은 상태의 엔트로피에서 feature를 통해 분류를 한번 거쳤을 때의 엔트로피를 뺀다. 분류를 거친다는 것은 질문을 추가적으로 하는 것과 같은 의미다. 따라서 이런 정보를 획득함에 따라서 전체의 엔트로피는 적어도 늘어나지는 않을 것이다. 둘 사이의 차이를 해당 feature가 지닌 정보 품질로 이해할 수 있겠다. 

![](https://github.com/anarinsk/public_writing/raw/master/entropy/imgs/data.png)




위와 같은 학습 자료가 주어졌다고 하자. 맞추고자 하는 정보는 테니스는 칠 것인지 말 것인지의 여부다. 
아무런 분류를 거치지 않았을 때 위 학습자료의 엔트로피는 다음과 같다. 전체에서 플레이를 한 횟수는 9번 하지 않은 횟수는 5번이다. 이는 일종의 이진 분류다. $S$는 

$$
\{ \text{No, No, Yes, Yes, Yes, , No, Yes, , No, Yes, Yes, Yes, Yes, Yes, No} \}
$$

이다. S의 엔트로피는 다음과 같다. 

$$
e(S) = -(\dfrac{9}{14} \log_2 \frac{9}{14} + \dfrac{5}{14} \log_2 \frac{5}{14} ) = 0.94
$$

이제 위의 자료에서 주어진 feature를 활용해서 IG를 구해보도록 하자. 여기서는 참고로 날씨(outlook)라는 하나의 feature에 대해서만 계산하도록 하겠다. 날씨 feature의 집합은 

$$
\{ \text{Sunny, Overcast, Rain} \}
$$ 

세 가지 원소를 지닌다. 그리고 이 원소에 대해서 각각의 $e(S_v)$는 다음과 같다. 

$$
\begin{aligned}
e(S_{\text{Sunny}}) &= -( \dfrac{2}{5} \log_2 \dfrac{2}{5} + \dfrac{3}{5} \log_2 \dfrac{3}{5}) \\
e(S_{\text{Overcast}}) & = 0 \\
e((S_{\text{Rain}}) & =  -( \dfrac{3}{5} \log_2 \dfrac{3}{5} + \dfrac{2}{5} \log_2 \dfrac{2}{5}) 
\end{aligned}
$$

$$
e(S_v) = \dfrac{5}{14} e(S_{\text{Sunny}})  +  \dfrac{4}{14} e(S_{\text{Overcast}})   +  \dfrac{5}{14} e(S_{\text{Rain}}) 
$$

이렇게 각 4개의 feature에 대해서 IG을 구하면 어떤 feature가 엔트로피를 더 낮추는지를 비교할 수 있다. 계산을 해보면 Outlook이 제일 높은  IG를 지니고 있다. 따라서 Outlook이 의사결정 나무에서 가장 상단에 위치하게 된다. 이제 1차 분류를 거친 후 각각 분류된 집합에 대해서 같은 방식의 분류를 반복한다. 분류는 더이상 분류될 것이 없을 때까지, 즉 주어진 집합의 엔트로피가 0이 될 때까지 반복한다. 엔트로피가 0이 된다는 것은 무슨 뜻일까? 해당 분류에 속하는 개체의 목표 속성이 같다는 말이다. 더 분류할 것이 없어질 때 분류가 멈춘다. 

![](https://github.com/anarinsk/public_writing/raw/master/entropy/imgs/tree.png)

### Reference 

1. [Wikipedia: Entropy_information](https://en.wikipedia.org/wiki/Entropy_(information_theory))
2. [A Mathematical Theory of Communication](http://math.harvard.edu/~ctm/home/text/others/shannon/entropy/entropy.pdf)
3. [Decision tree example](https://becominghuman.ai/decision-trees-in-machine-learning-f362b296594a)
:feet:
:feet:
:feet:
:feet:
:feet:Jun Sok Huhh | :house:[lostineonomics.com](http://lostineconomics.com)



















<!--stackedit_data:
eyJoaXN0b3J5IjpbNDc3Njk3ODA4LC04OTk5MjI3ODgsMTkwOT
c1ODI4LC0xNTE5ODMzNTU3LC03OTI2MjkwMiwtMTMwNTU0MTA5
OCwtNTI4NzcwNTc2XX0=
-->