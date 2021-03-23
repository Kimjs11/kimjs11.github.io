---
layout: posts
title:  "Code Error '[Jupyter notebook] IOPub data rate excceeded.'"
date:   2021-03-23 09:00:20 +0700
categories: [Code Error]
---
<link rel = "stylesheet" href ="/static/css/bootstrap.min.css">

--------------------------
~~~
IOPub data rate exceeded. The notebook server will temporarily stop sending output <br/>
to the client in order to avoid crashing it. To change this limit, set the config <br/>
variable `--NotebookApp.iopub_data_rate_limit`. <br/>
Current values: NotebookApp.iopub_data_rate_limit=1000000.0 (bytes/sec) NotebookApp.rate_limit_window=3.0 (secs)
~~~
<br/>
쉽게 보면 출력 데이터 초과시 발생하는 오류, 처리 속도를 조절해 주면 된다.<br/>

--------------------------
아래 명령어 입력해주면된다.<br/>
~~~
jupyter notebook --NotebookApp.iopub_data_rate_limit=1e10
~~~~
<br/>
아래 사이트를 참고하여 해결하였습니다.<br/>
https://stackoverflow.com/questions/43490495/how-to-set-notebookapp-iopub-data-rate-limit-and-others-notebookapp-settings-in?noredirect=1&lq=1
