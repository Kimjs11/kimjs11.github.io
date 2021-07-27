---
layout: posts
title:  "(3)RuntimeError: DataLoader worker (pid 5787) is killed by signal: Bus error. It is possible that dataloader's workers are out of shared memory. Please try to raise your shared memory limit."
date:   2021-07-27 09:00:20 +0700
categories: [Code Error]
---
<link rel = "stylesheet" href ="/static/css/bootstrap.min.css">

--------------------------

~~~
RuntimeError: DataLoader worker (pid 5787) is killed by signal: Bus error. It is possible that dataloader's workers are out of shared memory. Please try to raise your shared memory limit.
~~~
<br/>

컨테이너 내부에서 네트워크 실행시, 메모리가 부족하여 실행되지 않게 됨.
<br/>
1)'shm'파일이 컨테이너에서 공유하는 폴더<br/>
2)df -h을 실행하여 'shm' 파일의 용량을 할당하기<br/>
3)컨테이너 생성시 '--shm-size 2G' 를 추가하여 용량을 할당<br/>
~~~
docker run -itd --name test **--shm-size** 2G -v/home/ubuntu/jinsu/share:/root -p 7777:7777 --gpus all --restart=always pytorch/pytorch
~~~
