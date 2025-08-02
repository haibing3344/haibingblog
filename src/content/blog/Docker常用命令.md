---
title: 'Docker常用命令'
date: 2020-08-23 19:21:51
tags: [Docker]
published: true
hideInList: false
feature: 
isTop: false
categories: 'Docker' # 添加这一行
id: 'docker-commands' # 添加这一行
---

# docker images /列出本地镜像
```bash
docker images -a
docker images -q
```
```bash
    HB-MacBook-Pro:~ apple$ docker images
    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
    ubuntu              latest              a2a15febcdf3        2 months ago        64.2MB
    ubuntu              14.04               2c5e00d77a67        5 months ago        188MB
```
# docker search /搜索镜像
```bash
docker search tomcat
```
```bash
    HB-MacBook-Pro:~ apple$ docker search tomcat
    NAME                          DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
    tomcat                        Apache Tomcat is an open source implementati…   2540                [OK]
    tomee                         Apache TomEE is an all-Apache Java EE certif…   69                  [OK]
    dordoka/tomcat                Ubuntu 14.04, Oracle JDK 8 and Tomcat 8 base…   53                                      [OK]
    bitnami/tomcat                Bitnami Tomcat Docker Image                     29                                      [OK]
    kubeguide/tomcat-app          Tomcat image for Chapter 1                      27
    consol/tomcat-7.0             Tomcat 7.0.57, 8080, "admin/admin"              16                                      [OK]
    cloudesire/tomcat             Tomcat server, 6/7/8                            15                                      [OK]
    aallam/tomcat-mysql           Debian, Oracle JDK, Tomcat & MySQL              11                                      [OK]
    arm32v7/tomcat                Apache Tomcat is an open source implementati…   9
    rightctrl/tomcat              CentOS , Oracle Java, tomcat application ssl…   5                                       [OK]
    maluuba/tomcat7-java8         Tomcat7 with java8.                             4
    unidata/tomcat-docker         Security-hardened Tomcat Docker container.      4                                       [OK]
    amd64/tomcat                  Apache Tomcat is an open source implementati…   2
    arm64v8/tomcat                Apache Tomcat is an open source implementati…   2
    i386/tomcat                   Apache Tomcat is an open source implementati…   1
    camptocamp/tomcat-logback     Docker image for tomcat with logback integra…   1                                       [OK]
    99taxis/tomcat7               Tomcat7                                         1                                       [OK]
    oobsri/tomcat8                Testing CI Jobs with different names.           1
    ppc64le/tomcat                Apache Tomcat is an open source implementati…   1
    secoresearch/tomcat-varnish   Tomcat and Varnish 5.0                          0                                       [OK]
    appsvc/tomcat                                                                 0
    picoded/tomcat7               tomcat7 with jre8 and MANAGER_USER / MANAGER…   0                                       [OK]
    cfje/tomcat-resource          Tomcat Concourse Resource                       0
    jelastic/tomcat               An image of the Tomcat Java application serv…   0
    s390x/tomcat                  Apache Tomcat is an open source implementati…   0
```
# docker pull /拉取镜像
```bash
docker pull nginx
```

# docker rmi /删除镜像
```bash
docker rmi -f 镜像ID  /删除指定镜像
docker rmi -f $(docker search -qa) /删除全部镜像
```
<!-- more -->

# 启动容器
```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

### 启动交付式容器

-t 打开容器终端

-i  保持终端打开
```bash
docker run -it --name  xx image
```
```bash
    HB-MacBook-Pro:~ apple$ docker run -it a2a15febcdf3
    root@fe809bbcb339:/# ls
    bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```
### 列出正在运行的容器
```bash
docker ps [OPTIONS]
```
```bash
    HB-MacBook-Pro:~ apple$ docker ps
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
    fe809bbcb339        a2a15febcdf3        "/bin/bash"         51 seconds ago      Up 50 seconds                           funny_cartwright
    HB-MacBook-Pro:~ apple$ docker ps -a
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS                   NAMES
    fe809bbcb339        a2a15febcdf3        "/bin/bash"         5 minutes  ago       Exited (0) 39 seconds ago                           funny_cartwright
    9c93d87999d0        ubuntu              "/bin/bash"         44 minutes ago      Exited (0) 44 minutes ago                           eloquent_banach
    03362b0a0589        ubuntu              "/bin/bash"         8 weeks ago         Exited (255) 4 weeks ago    0.0.0.0:32769->80/tcp   nginx
    HB-MacBook-Pro:~ apple$ docker ps -l
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
    fe809bbcb339        a2a15febcdf3        "/bin/bash"         5 minutes ago       Exited (0) 50 seconds ago                       funny_cartwright
```
# 退出容器
```bash
    exit 容器停止退出
    ctrl+P+Q 容器不停止退出
```
# 启动容器
```bash
    docker start 容器ID或容器名
```
# 重启容器
```bash
    docker restart 容器ID或容器名
```
# 停止容器
```bash
    docker stop  容器ID或者容器名
    docker kill 容器ID或者容器名 /强制停止
```
# 删除已停止容器
```bash
    docker rm 容器ID
```

# 守护式进程启动容器
```bash
    docker run -d 镜像名或者镜像ID
```
后台运行必须有前台进程。

# 查看容器日志
```bash
    docker logs -f -t --tail 容器ID
```
# 查看容器内运行的进程
```bash
    docker top 容器ID
```
# 查看容器内部细节
```bash
    docker inspect 容器ID
```
# 重新进入正在运行的容器并交互
```bash
    docker attach 容器ID  /重新进入不启动新的进程
    docker exec -it 容器ID bashShell  /重新进入并启动新的进程
```
# 拷贝容器内文件到宿主机
```bash
    docker cp 容器ID:容器目录 宿主机目录
```