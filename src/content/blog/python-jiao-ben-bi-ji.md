---
title: 'Python脚本笔记'
date: 2022-02-15 16:37:35
tags: [Python]
published: true
hideInList: false
feature: 
isTop: false
categories: 'Python'
id: 'python-script-notes'
---


## 脚本项目生成依赖包清单



```shell
pip3 install pipreqs

进入项目主目录
pipreqs ./

生成requirements.txt

安装依赖库：
sudo pip3 install -r requirements.txt
```



## request脚本转换工具

https://curlconverter.com/#

![screenshot of the Chrome DevTools](https://curlconverter.com/images/screenshot.png)



## 脚本定时运行crontab

```shell
crontab [ -u user ] { -l | -r | -e }

参数说明：

-e : 执行文字编辑器来设定时程表，内定的文字编辑器是 VI，如果你想用别的文字编辑器，则请先设定 VISUAL 环境变数来指定使用那个文字编辑器(比如说 setenv VISUAL joe)
-r : 删除目前的时程表
-l : 列出目前的时程表
```

```makedown
*    *    *    *    *
-    -    -    -    -
|    |    |    |    |
|    |    |    |    +----- 星期中星期几 (0 - 6) (星期天 为0)
|    |    |    +---------- 月份 (1 - 12) 
|    |    +--------------- 一个月中的第几天 (1 - 31)
|    +-------------------- 小时 (0 - 23)
+------------------------- 分钟 (0 - 59)
```

```shell
0 */2 * * * /sbin/service httpd restart  意思是每两个小时重启一次apache 

50 7 * * * /sbin/service sshd start  意思是每天7：50开启ssh服务 

50 22 * * * /sbin/service sshd stop  意思是每天22：50关闭ssh服务 

0 0 1,15 * * fsck /home  每月1号和15号检查/home 磁盘 

1 * * * * /home/bruce/backup  每小时的第一分执行 /home/bruce/backup这个文件 

00 03 * * 1-5 find /home "*.xxx" -mtime +4 -exec rm {} \;  每周一至周五3点钟，在目录/home中，查找文件名为*.xxx的文件，并删除4天前的文件。

30 6 */10 * * ls  意思是每月的1、11、21、31日是的6：30执行一次ls命令
```

### 删除定时任务

查看已创建任务：

```shell
[root@VM-16-2-centos yokai]# crontab -l
*/5 * * * * flock -xn /tmp/stargate.lock -c '/usr/local/qcloud/stargate/admin/start.sh > /dev/null 2>&1 &'
[root@VM-16-2-centos yokai]#
```



进入命令配置界面：

```shell 
crontab -e
```
![](https://haibing.xyz/post-images/1645004369921.png)

vi编辑配置文件

:wq 退出保存

>  **注意：**当程序在你所指定的时间执行后，系统会发一封邮件给当前的用户，显示该程序执行的内容，若是你不希望收到这样的邮件，请在每一行空一格之后加上 **> /dev/null 2>&1** 即可，如：

```
20 03 * * * . /etc/profile;/bin/sh /var/www/runoob/test.sh > /dev/null 2>&1 
```

<!-- more -->
