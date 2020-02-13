---
title: "리눅스 기본 설정"
permalink: /develop/intern4
layout: category
---



----------------------------------------
# 리눅스 기본 설정들 - pip, python, pkg-config
--------------------------------


### 기본 pip 설정

-----------------------------

`$ ls /usr/local/bin/pip*`

를 하면 pip가 여러개 나옴.

/usr/local/bin/pip  /usr/local/bin/pip2.7 /usr/local/bin/pip3.5

/usr/local/bin/pip2 /usr/local/bin/pip3



기본 pip로 설정하고 싶은 것을 복사해서 pip로 설정.

` sudo cp /usr/local/bin/pip2.7 /usr/local/bin/pip`



`$ pip -V` 를 통해 어떤 버전이 기본인지 알 수 있음.



### 기본 python 설정

------------------------------------------

python3를 기본으로 설정 : 

`vi ~/.bashrc`

`alias python=python3`



이게 가끔 안될때가 있는데..

안되면

`sudo update-alternatives --config python` 으로 파이썬 목록을 본 후

`sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 10`

원하는 파이썬 버전에 높은 우선순위를 부여한 뒤

`sudo update-alternatives --set python /usr/bin/python3.6`

설정을 한다.



### pkg-config

----------------------------

pkg-config *opencv(라이브러리 이름)* --cflags --libs : 컴파일시 필요한 라이브러리 모두 출력 (매우 편함)



makefile시에 사용하면 매우 편함.

ex)

``` 
OPENCV = `pkg-config opencv --cflags --libs``

PYTHON = `pkg-config python3 --cflags --libs`

LIBS = $(OPENCV)

PLIBS = $(PYTHON)
```

이렇게 쓰면 opencv, python3를 사용할 때 필요한 것들을 다 불러옴.