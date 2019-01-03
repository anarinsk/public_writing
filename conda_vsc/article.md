**Python + Visual Studio Code**

2018-11-23
Jun Sok Huhh | :house:[lostineconomics.com](http://lostineconomics.com), also posted at [LINK](https://danbi-ncsoft.github.io/etc/2018/11/26/conda_vsc.html)설정하기 

# 들어가며 
아마 각자 알아서 잘 쓰는 Python 설정이 있을 것이다. 그대로 잘 쓰면 되겠다. 하지만 막 Python으로 코딩을 시작하려는 사람이 있다면 이런 글도 조금은 도움이 되지 않을까 한다. 이 가이드의 목표는 다음과 같다. 

0. 되도록 꼬이지 않게 Python 쓰기 (사실 쓰다보면 종종 꼬인다)파이썬 쓰기 
1. 되도록 편리하게 쓰기 
2. OS를 가리지 않고 쓰기 

Python파이썬이 무척 훌륭한 언어지만 사실 가이드가 아주 친절하지는 않다. 입문서들을 봐도 혹은 웹서핑을 해봐도 그렇다. 아울러 같은 오픈소스 언어라도 RStudio와 같은 편리한 개발툴까지 손에 쥐어주는 R에 비해서 어딘가 불편하고 부족하다는한 느낌도 받을 수 있다. Python을 쓰면서 불편하다고 느껴본 적 없다, 라는 분들은 여기서 이 글을 안 읽어도 좋겠다. 

이 가이드는 거의 R + RStudio에 근접한 수준으로 Python을 쓰게 하는 데 필요한 작업을 다룬이 가이드를 통해서 거의 R + RStudio에 근접한 수준으로 파이썬을 쓰게 되기까지 개인적으로 삽질한 내용의 핵심만을 제시하고자 한다. 부디 이 글을 보는 분들에게 시간 단축의 축복 있으라! 가이드는 다음과 같은 세가지 영역을 다룬다. 

1. 어떤 Python 배포판을 쓸까 것인가? 
2. 어떻게 쓸까 것인가? 
3. 무엇과 함께 쓸까 것인가? 

# 어떤 Python 배포판을 쓸까 것인가? 

나는 하드코어하게 그냥 바닐라 Python파이썬을 쓰겠어, 라고 결심해도 좋겠다. 하지만 곧 여러가지 장애물을 만나게 될 것이다. 특히 윈도를 쓰는 이용자라면 더욱 그렇다. CLI(command line interface)를 맥OS나 리눅스 만큼 자유롭게 쓸 수 없기에 답답할 때가 많다. 게다가 PATH 걸기 등에서 문제가 생기면 꽤참 난감하다. 또한 각종 패키지 또한 누가 한번 더 걸러서 잘 관리를 해주고 그 녀석들을 끌어다 쓰면 조금 더 편리하게 쓸 수 있지 않을까 싶다. 이러한 목적에 딱 맞는 것이 아나콘다(Anaconda) 사에서 배포하는 아나콘다Anaconda 배포판이다. 아마도 Python을 쓰는 사람이라면 아나콘다를 한번쯤은 깔아보았을 터다. 우리도 아나콘다를 쓸 것이다. 아나콘다 배포판이 좋은 이유는 두 가지 정도다. 

1. 아나콘다에서 패키지 관리를 성실하게 해준다. 
	- 때로는 바닐라 버전보다 아나콘다 버전이 성능상 유리한 경우도 있다. 
2. 아나콘다에서 제공하는 가상 환경이 편리하고 훌륭하다. 
	- virtualenv 패키지를 써도 좋겠지만 패키지 관리까지 한방에 해결할 수 있는 아나콘다 가상환경이 조금 더 편리2. 아나콘다에서 제공하는 가상 환경이 편리하고 훌륭하다. 

1이야 그렇다고 치고 2는 정말 중요하다. 보통 "Python + 필요은 핵심을 이루는 프로그램이 가볍다. 대신 필요에 따라서 여러가지 패키지"를들을 깔아서 쓰고 있을 것이다. 하지만 이렇게 여러쓴다. "Python + 패키지"를 깔면 깔수록 무거워지고 문제가 발생할 소지가 높다. 만일 작업 환경을 필요에 따라서 분리해 관리한다면,구축한 후 이 환경 내에서만 쓰면 여러가지 이점이 있다. 일단 뭔가 문제가 생겼을 때 이 환경만 날려버리면 된다. 패키지 하나 잘못 깔았다고 낙담할 필요가 없다. 아울러 필요한 구성만 갖추기 때문에 다른 측면실행 속도 등에서도 약간의 이익을 볼 수 있다. 

이제 아나콘다를 쓰기로 했다고 치자. 아나콘다는 두 가지로 배포판이 제공된다. 종합 배포판인 아나콘다 대신 핵심 만을 발라낸 [Miniconda](https://conda.io/miniconda.html)를 권한다. 미니콘다가 왜 좋을까? 보통 아나콘다를 풀 버전을 깔면 (내 기준으로는) 쓸 데 없는 것들이 같이 깔린다. 일종의 합집합 개념의 여러 소프트웨어를 제공하는데, 아나콘다 회사에서 권장하는 방식에 꼭 적응해야 할 필요는 없다. 예를 들어, 개발 환경으로 Spyder를 쓰지 않는데 깔 필요는 없지 않을까? 하드 디스크의 용량이 부족한 시대는 아니지만, 잘 쓰지 않는 것을 갖고 있을 필요도 없다. 

# 어떻게 쓸까 것인가? 

일단 미니콘다를  Python 3.xX 버전으로 (전부 "Next"를 눌러디폴트로) 깔았다고 가정하자. 대신 미니콘다를 쓰려면 약간의 CLI를 활용할 줄 알아야 한다. 맥OS나 리눅스에서는 그냥 터미널을 열고 쓰면 되니, 윈도 기준으로 설명하겠다. 

<kbd><img src="https://github.com/anarinsk/public_writing/blob/master/conda_vsc/imgs/conda_prompt.png?raw=true" width="200"></kbd>

일단, 탐색창에서 anaconda prompt를 검색하면 다음과 같이 뜬다. 윈도우에서 발생할 수 있는 각종 문제를 해결한 아나콘다 터미널이라고 생각하면 되겠다. 앞으로 아나콘다 관련 명령어들은 이 녀석을 띄우고 실행시키면 된다.  

아나콘다의 각종 명령어에 대한 자세한 해설은 링크와 같다. 하지만 엑기스만 뽑아서 간단히 설명하도록 하자. 창을 실행하면 "(base)"라는 문구가 보일 것이다. 이는 현재 아나콘다가 실행되고 있는 환경을 뜻한다. 이미 Python파이썬 가상환경이 들어와 있다! Miniconda의 클라이언트와 함께 Python파이썬 3.xX 버전이 깔려 있고 녀석을 기본으로 쓰겠다는 의미다. 

- conda의 활용법을 자세히 알고 싶다면 [LINK](https://conda.io/docs/user-guide/getting-started.html)를 참고하라. 
- 가상 환경에 관한 자세한 내용은 [LINK](https://conda.io/docs/user-guide/tasks/manage-environments.html)를 참고하라. 

## For Windows 

VSC 안에는 사실 터미널도 들어 있다. conda prompt를  VSC 안에서 한번에 실행할 수 있다면 좋지 않을까? 메뉴를 뒤져 터미널을 실행시키고 콘다 명령어를 실행시켜보자. 아마 에러가 뜰 것이다. 현재 VSC가 호출한 터미널은 윈도 기본 터미날이고, 여기에는 conda가 세팅되어 있지 않기 때문에 생기는 일이다. 어떻게 해야 할까? 

- conda prompt의 실행 환경을 바꾸자. 녀석이 각종 패키지를 깔고 하드를 조작할 수 있으려면 관리자 권한이 부여되어야 한다. "바로가기" 탭에 고급에서 설정할 수 있다. 
- 두번째로 "바로가기" 탭에 대상 항목의 내용을 복사해두자. 여기 내용은 conda prompt를 실행할 수 있는 구체적인 명령어가 담겨 있다. 이 글을 쓰는 컴퓨터의 세팅에서는 아래와 같다. 

```cmd
%windir%\System32\cmd.exe "/K" C:\ProgramData\Miniconda3\Scripts\activate.bat C:\ProgramData\Miniconda3
```

- VSC에서 File &rarr; Perefrences &rarr; Settings로 간다. 그러면 아래 스크린 샷과 같은 설정화면이 나타난다. 
  - 검색창에 "terminal"을 치면  Features 아래 Terminal을 고르고 우측 창에서 "Edit in settings.json"을 선택한다. 
  - 그리고 아래 스크린샷처럼 세팅 아래 위에서 복사한 주소를 넣는다. 주의할 점은 아래와 같이 되도록 넣어야 한다. 

```
```

- 이제 VSC에서 terminal을 실행하면 conda prompt와 동일한 환경이 뜬다. 

## Update Conda 

```cmd
conda update conda
```
- 매번 콘다를 실행하고 실행해야 할 명령이다. 
-음을 뜻한다. 항상 콘다를 실행하고 나면 먼저 실행해야 할 명령어는 `conda update conda`이다. 아나콘다 배포판을 관리하는 메타툴이 conda이고 이 녀석을얘를 업데이트하라는 뜻이다. 제 머리 깎는 중인 셈이다. 

## Create 

```cmd
conda create -n 환경이름 python=3.6
```

- 앞으로 사용자가 각자 지정해주는 부분은 한글로 표기하도록 한다. 여기서는 "환경이름"이 이에 해당한다. 
- `create` 명령어에 여러가지 옵션이 있지만 여기서는 Python 버전만 지정하도록 하겠다. 
- 이렇게 설치된 아나콘다의 환경은 윈도우 기준으로  `ProgramData\Miniconda3\envs` 에 설치되어 있다. ProgramData가 보통 숨은 폴더 처리가 되어 있다. 이 폴더를 보려면 탐색기 옵션을 고쳐야 한다. [LINK1](https://support.microsoft.com/ko-kr/help/14201/windows-show-hidden-files), [LINK2](https://support.microsoft.com/ko-kr/help/4028316/windows-view-hidden-files-and-folders-in-windows-10)를 참고 하라. 

## Activate env, and...

다음으로 환경으로 진입해야 한다. 

```cmd
conda activate 환경이름
```

위의 명령어는 윈도우 기준이다. 맥OS나 리눅스는 `source activate 환경이름`을 쓰면 된다. 이제 원하는 패키지를 깔면 된다.

```cmd 
conda install -c conda-forge numpy
```
 
 사례로 numpy 패키지를 깔아 보았다. 위 명령어는 conda 명령어로 anaconda-forge 채널을 통해 numpy를 설치한 것이다. 통상적으로 pip 명령어를 써서 패키지를 인스톨해도 상관없다. 

## View env  

```cmd
conda info --envs 
```
 - 현재 콘다 내에서 사용할 수 있는 환경을 보여준다. 
 
## Remove env 
 
환경에 문제가 생겼을 경우 이렇게 지우면 된다. 

```cmd
conda env remove -n 환경이름
```

- 아니면 앞서 봤던 폴더에 환경 이름의 폴더를 지워도 된다. 
- env의 이름을 바꾸고 싶으면 해당 폴더의 이름을 바꿔주면 된다. 

## Copy env 

이미 설치된 환경(클론되는환경)을 다른 이름(클론될환경)으로 카피하고 싶으면 아래의 명령어를 활용하자. 

```cmd
conda create -n 클론될환경 -c 클론되는환경
```
- 환경을 복제하고 싶으면 그냥 해당 폴더를 복사에 붙인 후 다른 이름을 붙여주면 된다. 

## Enter your env

이제 필요한 패키지들을 깔아서 쓰면 된다. 그전에 잠깐! 필요한 패키지들은 해당 환경 안에 깔아줘야 의도한 대로 쓸 수 있다! 환경에 진입하도록 하자. 

```cmd 
conda activate 환경이름
```

환경에서 나가기 위해서는 

```cmd 
conda deactivate 환경이름
```

- 윈도에서는 이렇게 하면 된다. 요즘 miniconda 윈도 버전에서는 conda 명령어를 생략해도 환경에 잘 진입된다. 
- 맥OS나 Linux라면 `conda`  대신 `source`를 치면 된다. 

# 무엇과 함께 쓸까? 

이제 conda와 잘 어울리는 짝으로는 MS에서 무료로 배포하는 Visual Studio Code(VSC)를 권한다. 개인적으로 마소에서 낸 제품 중 최고의 걸작이 아닐까 싶다. VSC에 대한 자세한 설명은 생략하자. 

Python을 VSC와 함께 쓸 때의 장점은 다음과 같다. 

- 여느 에디터의 장점들
	- 다양한 테마
	- 단축키 
	- 탭으로 필요 명령어 채우기 
	- 내부에서 터미널(cmd)를 실행 가능 
- Git이 통합되어 있어서 git 관리가 편리
- 다양한 익스텐션과 편리한 설치
- conda 환경을 지정해 실행 가능 
- Jupyter의 환경을 그대로 가져와서 실행 결과를 바로 보여주기 

이런 것들을 구현해주기 위해서 작업 환경에 두가지 패키지를 깔면 된다. 

- Jupyter or Jupyerlab 
- pylint 

생성한 작업환경 내에서 아래와 같이 두 개의 패키지를 설치한다. 

```cmd 
conda install -c conda-forge jupyterlab
conda install -c conda-forge pylint
```

pylint의 경우 해당 conda 환경에 안 깔려 있으면 VSC에서 깔지 않겠느냐고 물어보고, conda로 깔지 pip로 깔지까지 물어본다. 혹시 생략했다면 VSC안에서 처리가 가능하다. 

이렇게 깔아 놓고 `*.py`을 불러오자. 에디터 창에서 매직코멘트로 `#%%`을 쓴다. 매직 코멘트는 pylint 패키지가 해당 명령어를 Jupyter로 넘길 수 있도록 지정한다. VSC에서 pylint가 제대로 작동한다면 매직 코멘트 위로 다음과 같은 화면을 보게 될 것이다. 

<kbd><img src="https://github.com/anarinsk/public_writing/blob/master/conda_vsc/imgs/pylint.png?raw=true" width="500">
</kbd>

빨간색 박스에너 "Run Call"은 해당 매직코멘트 블록을 실행하라는 의미다. Jupyter 내에서 한 블록으로 이해하면 된다. pylint의 작동원리는 해당 코멘트를 Jupyter로 넘겨 실행한 후 이를 받아서 다시 VSC 내에 뿌려준다. 결과는 아래와 같이 제법 번듯하다! 화면의 오른쪽 창은 jupyter의 실행 결과와 동일하다. 

<kbd><img src="https://github.com/anarinsk/public_writing/blob/master/conda_vsc/imgs/vsc_1.png?raw=true" width="700">
</kbd>

앞서 conda를 통해서 다양한 가상 환경을 설치했다면 이 환경을 선택해 VSC에서 실행할 수 있어야 할 것이다. 위의 창에서 맨 아래 보라색 줄을 보자. 

<kbd>
<img src="https://github.com/anarinsk/public_writing/blob/master/conda_vsc/imgs/vsc_2.png?raw=true" width=450>
</kbd>

저 위치를 클릭하면 에디터 위쪽으로 아래 같은 화면이 뜬다. 화면에서 해당 conda 환경을 선택하면 된다. 

<kbd><img src="https://github.com/anarinsk/public_writing/blob/master/conda_vsc/imgs/vsc_3.png?raw=true" width=600></kbd>

## 주의 사항 

가끔 콘다 환경을 세팅한 후 해당 환경이 VSC에서 안뜨는 상황이 발생할 수 있다. 그럴 때에는 해당 환경에 pylint가 설치되어 있는지 확인한 후 설치되어 있다면 환경 선택 부분에 리로드 아이콘을 눌러주자. 그냥 에디터를 다시 실행해도 된다. 그러면 해당 환경을 확인해 선택할 수 있을 것이다. 

# A nice practice 

이렇게 쓰면 좋다,라는 모델 케이스를 정리해보자. 물론 "이게 최선"은 아니겠지만, 그래도 꽤 삽질을 거친 결과니 참고하면 좋을 듯 하다. 가장 번거롭고 난이도가 높은 윈도 기준이다. 

1. miniconda 설치 
2. VSC 설치 
3. miniconda에 Python 작업 환경 설치 및 환경별 패키지 설치 
4. VSC 실행 
5. 필요한 `*.py` 생성 혹은 로딩 
6. VSC를 통해 작업 

## One more tip

매번 이렇게 환경을 설치해서 쓰기 귀찮을 수 있다. 그렇다면 많이 쓰는 공통 세팅을 하나 만들어 두고 이 녀석을 복사해서 쓰면 되겠다. 앞서 보았듯이 `conda create`.. 명령으로 환경을 복사해서 쓰거나 아니면 그냥 폴더/디렉토리로 들어가서 내용을 복사한 뒤 이름을 바꾸면 된다. 실은 나도 그렇게 쓰고 있다.[^1]

[^1]: 이것은 시험이다! 

아울러 코드를 배포할 일이 있을 때 실행 환경을 담보해야 할 것이다. 이럴 때는 yml을 쓰면 좋다. 

### yml 사용하기 
yml 파일을 생성해서 한방에 패키지들을 설치하는 방법은 다음과 같다. 

```cmd
conda env export > 환경이름.yml
```

현재 환경을 yml 파일로 저장한다. 해당 yml을 다시 환경으로 풀려면

```cmd 
conda env create -f 환경이름.yml
```

해당 yml 파일에서 환경을 복원한다. 작업한 환경을 yml로 포팅해 두면 패키지의 버전까지 기억했다가 그대로 복원한다. 
:feet:
:feet:
:feet:
:feet:
:feet:Jun Sok Huhh | :house:[lostineonomics.com](http://lostineconomics.com)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzczMzc5MDgzLDE3Njk0NDc3MjgsLTIwOD
gxNDk0LDE2MzQxNDIyNzAsLTQ0MTgxNzQyOCwtODAwODYzODQs
LTE4NzkwODQ2NTIsLTk5OTE4Mzk0OSwxMjg4NjYwNjAxLDIxMz
Q5NjYyODMsMTg5MzM1MzM0Niw1NDUzMTI4OTAsLTE1NjE1NjA0
ODQsMTkxODU4NTEwMiwzNTgxNzAxMCwtMTE5MTc4MzQxMSwzMT
E3NzI4OCwtMTc5NzM0MjMyNiwtMTAxODM3ODQ4NCw3NTI4ODIy
NzldfQ==
-->