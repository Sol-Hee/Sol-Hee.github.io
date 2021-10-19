---
title: MAC 의 Python version 관리
excerpt: With MAC Python 기본 버전 관리

categories:
  - Python
tags:
  - mac
  - jupyter
  - version
---

🔥 다음 번 환경세팅할 때 삽질하지 않기 위하여 기록....
{: .notice--danger}

## MAC은 기본적으로 Python 2.7이 내장되어 있다.
하지만 ! 2.7버전은 2020년 초에 이미 업데이트 종료되었다. <br/>
**그리고 나는 2.대 버전을 사용 해본 적이 단, 한번도 없었다....**<br/>
그러나 구글링을하며 2.대 버전을 MAC에서 지우면 문제가 생긴다고 했던 글을 본 적이 있다.<br/>
따라서, 3.대 버전을 설치 후 환경변수를 설정해주면 된다.

## 절차 
📌 세팅 : Python 공식 홈페이지에서 설치, pip 사용
### 1. 원하는 파이썬 버전 설치
나의 경우, [Python 공식 홈페이지](https://www.python.org/downloads/) 에서 3.7.2를 받았다.
(이 버전이 사용한 것들 중 안정감이 있는 것 같다, ~~괜히 검색하면 3.7이 많이 나오는게 아닌가보다ㅋㅋ~~)

### 2. 환경변수 세팅  
환경변수는 늘 나를 힘들게.....한다....ㅋㅋ 🤬<br/>
**1. zsh, bash 중 default 실행 환경 확인한다. (나의 경우 zsh 였따.... 회사 컴은 bash 였는데 'ㅅ')**<br/>
😇 확인 방법
```bash
# shell 변환 시 default 어떤 것인지 출력 되었다.
$ chsh -s /bin/bash
$ chsh -s /bin/zsh

# 현재 실행창 확인
$ ECHO $SHELL
```

**2. 해당하는 shell vi file 접속** 
```bash
# bash
$ vi ~/.bash_profile
# zsh
$ vi ~/.zshrc
```

**3. 환경변수 추가**
```bash
# Setting PATH for Python 3.7
# Thr original Version is saved in .zshrc.pysave
export PATH=/Library/Frameworks/Python.framework/Versions/3.7/bin:$PATH
alias python="python3"
```
- alias 는 python3 <명령어> 대신 python <명령어> 커맨드여도 python3 버전이 실행되게 하는 것

**4. 부어 부어!**
```bash
$ source ~/.zshrc
```

이후 python --version 확인해보면 3.버전이 출력되는 것을 확인할 수 있다.

## Jupyter Python 버전 관리
나는 주피터 실행환경이 Python@특정버전 위에 올라가는 줄 알았는데,
그게 아닌 모든 Python 버전들이 다대일로(함수 생각하면,, X:Python@versions, Y:Jupyter)연결되는 구조였다.(~~어쩐지 자꾸 버전 2.7로 잡히더라 후..~~)
<br/>
아래 커맨드를 실행해주면 주피터에 {NAME}의 커널이 추가된다.

```bash
python3.7 -m pip insatll ipykernel
python3.7 -m ipykernel install --user --name="{NAME}"
```

- jupyter 실행환경 파이썬 버전 확인

```python
import sys
print(sys.version)
```

# 끝 !
~~이제 삽질 금지~~