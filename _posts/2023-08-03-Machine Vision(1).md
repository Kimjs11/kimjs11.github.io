---
layout: posts
title:  "(1)Machine Vision 이란"
date:   2023-08-03 09:00:20 +0700
categories: [Machine Vision]
---
<link rel = "stylesheet" href ="/static/css/bootstrap.min.css">


--------------------------
<br/>
### 머신 비전이란 ###

<br/>
카메라 센서를 통해 물체의 형상을 인지 및 인식하고 이미지 처리 기법을 통해 타겟 물체(생산품, 부재)의 계측으로 사용

<br/>
이전 포스터에서는 remote-SSH 프로그램"Xshell"을 통한 Linux 환경을 원격으로 접속하여 Docker를 연결하고 사용함. <br/>
이번 포스터에서는 로컬PC에서 VS code를 이용하여 docker 연결 및 컨테이너 생성을 하는 것을 해보고자 함. <br/>
<br/>

docker 를 설치했다면 'ctrl+ `', 'ctrl+ ~' 를 누르면 VS code 하단에 TERMINAL 창이 생성 <br/>
<br/>
image 검색 <br/>
~~~
docker images
~~~
<br/>
~~~
docker run -itd --name [컨테이너 명] -v d:\vscode:/root -p 8888:8888 --restart=always [이미지 명]
~~~
-itd<br/>
: 입출력/쉘 관련 옵션, -d : background 해당 옵션을 넣지 않으면 컨테이너 시작 후, 후속 명령어만 입력되고 exit 되버림.<br/>
-v<br/>
: 로컬 PC(D 드라이브) <-> 컨테이너(root 폴더)간 Mount를 해서 실시간 동기화
<br/>

~~~
docker exec -it [컨테이너 명] bash
~~~
