---
layout: posts
title:  "docker 내 RuntimeError: CUDA out of memory."
date:   2022-05-27 09:00:20 +0700
categories: [Code Error]
---
<link rel = "stylesheet" href ="/static/css/bootstrap.min.css">

--------------------------
<br/>
~~~
RuntimeError: CUDA out of memory.
~~~
<br/>
~~~
docker run --name jinsu -p 8888:8888 **--ipc=host** -v /mnt/disk0/:/root [image name]
~~~
docker run 실행시 --ipc=host를 <br/>
참고사이트<br/>
https://curioso365.tistory.com/136
