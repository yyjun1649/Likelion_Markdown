# Django Setting

python 설치 -> git 설치 - > Visual Code 설치



### CLI -> GUI


GUI의 단점 : 처음 지정된 기능 밖에 사용 불가, 조작속도가 CLI에 비해 늦은 경우가 있음

-> 이를 해결하기위한 방법 : 터미널

![image-20210531130710482](C:\Users\YOON YOUNGJUN\AppData\Roaming\Typora\typora-user-images\image-20210531130710482.png)



Home(~) : 터미널 구동 시 처음 위치하는 디렉터리

Working directory(.) : 작업중인 현재 위치

Root directory(/) : 디렉터리의 시작점

상위 디렉터리(..) 하위 디렉터리 : 상대적





옵션 : "-"로 시작해서 영문대 소문자로 구성, 명령어의 기능을 구체화, 명령어에 따라 없을수도 있음.



pwd : 현재위치를 알려줌

man : 명령어 설명서 

ls: 디렉터리의 목록을 보여줌

- 옵션 a : 숨김파일까지 보여줌
- 옵션 l : 파일의 상세정보
- 옵션 F : 파일인지 디렉터리인지 알려줌



cd : 현재 위치를 이동해줌

clear : 터미널 초기화

history : 이전에 사용했던 명령어들을 보여줌

tab을 누르면 자동으로 명령어를 입력해줌



Python 2.7 , Django 2.2



Python 3.7 , Django 3.1



python -m venv name : 가상환경 생성

source myvenv/Scripts/activate : 가상환경 실행

pip install django : django 다운로드

django-admin startproject name : name프로젝트 생성

cd 사용하여 가상환경으로 이동

python manage.py runserver : 서버실행 