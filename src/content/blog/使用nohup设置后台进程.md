---
title: '使用nohup设置后台进程'
date: 2020-08-21 18:20:38
tags: [linux]
published: true
hideInList: false
feature: 
isTop: false
categories: 'Linux'
id: 'nohup-background-process'
---

    引言： 有时候需要在Linux上设置一个后台进程，但是当你关闭terminal之时，它会被系统kill掉，那该如何来实现其后台进程能一直运行下去呢？

## 使用方式

    nohup command-with-options &

当在屏幕上敲击上述命令之后，屏幕上会出现如下信息：

    $ nohup: ignoring input and appending output to `nohup.out’

敲击回车，就退出了nohup.out当前的界面，进入正常的命令行。


## 输出日志信息

接下来的输出的日志信息，将输出到nohup.log.即将屏幕上输出的日志信息直接输出到nohup.log文件。

## 后台进程的标识符
如果一个命令只使用&来标识，则表示其在当前Session中，运行在后台。如果当前Session关闭或者当前的terminal工具关闭，则其附属的进程将会关闭。

## 总结
正常运行的后台进程都是需要nohup与&，两者并行使用的，方可保证其在后台正常运行。

## 查看后台任务

jobs -l

    jobs -l

    [1]  + suspended  nohup python3 fang.py

## 后台任务转前台
fg %任务编号

    (base) apple in ~/py λ fg %1

    [1]  + 1000 continued  nohup python3 fang.py

---

版权声明：本文为CSDN博主「bladestone」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/blueheart20/article/details/78226066