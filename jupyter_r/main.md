# Jupyter? 

R에는 이미 RStudio라는 훌륭한 개발환경(IDE: Integrated Development Environment)이 있다. R을 쓰는 사람이라면 여러가지 프로젝트 관리, 편리하고 일관된 객체(데이터 프레임 등) 뷰어, 순차 실행 등의 훌륭한 기능을 제공하는 RStudio 외에 다른 도구를 떠올리기 힘들 것이다. Python에도 RStudio를 본딴 IDE가 있을 정도니 그 우수성을 새삼 강조할 필요가 없겠다. 

그렇다면 왜 Jupyter(혹은 Ipython)에 관심을 두어야 할까?  나부터도 Jupyter하면 절로 Python이 떠오른다. 그런데 Jupyter는 Python에서만 쓸 수 있는 도구가 아니다. Jupyter는 웹 브라우저에서 돌아가는 인터프리터 스타일(인터랙티브)의 뷰어에 가깝다. 혹자는 농담 반 진담 반으로 Jupyter가 Julia + Python + R의 약자를 따서 만들었다고 주장하기도 했다.  Jupyter를 R과 쓰지 못한 이유는 없다. 

## 가벼운 실행 환경 

R이든 Python이든 가볍게 쓰려면 그냥 뭔가 뚝딱 되는 것이 좋다. Jupyter의 가장 큰 매력은 별도의 클라이언트 없이 웹 브라우저에서 돌아간다는 것이다. 페이지 열고 리소스를 호출할 수 있는 url을 주소창에 치면 끝이다. 가벼운 실행 환경이 필요한 다른 대목도 있다. 만일 로컬 데스크탑에 개발 도구를 설치하는 대신, AWS,  DigitalOcean  혹은 이용 중인 사설 서버에 개발 환경을 설치한다고 해보자. 일단 설치가 가벼워야 한다. 용량이 크거나 설치가 까다로우면 진입장벽이 높아진다. 일종의 서버 버전 Jupyter인 JupterHub가 일단 이 점에서 매우 만족스럽다. 

## 모바일 환경 

만일 실행 환경만 문제라면 RStudio 역시 웹브라우저에서 구동 되는 서버 버전인 RStudio Server를 제공한다. 스탠드얼론 버전과 동일한 기능을 제공하기 때문에 부족함에 전혀 없다. 원격으로 작업할 때 모바일은 반드시 고려할 수 밖에 없는 요소다. 급하게 코드를 스마트폰, 태블릿으로 보거나 수정해야 하는 상황이라면? 다양한 기능은 여기서 오히려 독이 된다. 

안드로이드에서는 별 문제가 없지만 iOS의 경우 OS의 이슈로 인해서 외부 키보드로 RStudio Server에 접근할 경우 방향 키가 먹지 않는다. 작은 화면을 제외하더라도 편하게 작업하기 힘들다.  Jupyter의 경우 iOS에서는 꽤 쓸만한 앱이 있다. Juno라는 앱은 주피터 서버와 iOS를 매끈하게 연결해준다. 외부 키보드 작업에도 아무런 문제가 없다. 

## 편리한 문서 작성 및 문서 공유 

R에서 rmd라는 포맷을 통해서 쉽게 코드+문서 환경을 구현할 수 있다. R을 기준으로 봤을 때에는 편리하고 다양한 것을 구현할 수 있는 도구지만, 그 자체로 그리 가볍진 않다. Jupyter는 코드와 markdown 환경을 자유롭게 오갈 수 있으면서도 가볍고 경쾌하다. 뚝딱 무엇인가를 시도하기에는 Jupyter가 부담이 덜하다. 아울러 Jupyter notebook은 github에서 문서 그대로 잘 보인다. 즉, 해당 주소를 그냥 공유해도 의사소통에 아무런 문제가 없다는 뜻이다. 이 점 역시 rmd 포맷에 비해 jupyter가 지닌 장점이다. 

# 설치 방법 

먼저 이용하려는 머신에 Jupyter가 깔려 있다고 전제하겠다. Python을 이용하는 환경이라면 터미널에서 `pip install` 혹은 `conda install` 등을 활용해 알맞게 인스톨하도록 하자. 앞서 언급했듯이 Jupyter는 언어를 태울 수 있는 일종의 옷과 같은 것이다. 따라서 올릴 수 있는 커널(언어)로 R을 인식시켜줄 수만 있으면 된다. 이를 위해 R에서 IRkernel 패키지를 설치하고 `installspec`을 한번만 실행하면 된다.  

```r
devtools::install_github('IRkernel/IRkernel')
IRkernel::installspec()
```

![](https://raw.githubusercontent.com/anarinsk/public_writing/master/jupyter_r/assets/images/jupyter_1.PNG)

이렇게 하면 Jupyter 환경에서 위 그림처럼 R 커널을 선택할 수 있다. 이제 커널을 선택하고 RStudio에서 쓰듯이 R을 쓰면 된다.  

예시 문서: [LINK](https://github.com/anarinsk/public_writing/blob/master/jupyter_r/assets/jupyter_r_example.ipynb)

# 참고 자료 

* [https://www.datacamp.com/community/blog/jupyter-notebook-r](https://www.datacamp.com/community/blog/jupyter-notebook-r)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg5MDM5NjMxMiw5MDE1MzM5NjcsMTQwMT
QyNjM5OSw2MDc4MTcwMjldfQ==
-->