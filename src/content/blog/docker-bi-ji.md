---
title: 'Docker笔记'
date: 2021-03-21 21:33:38
tags: []
published: true
hideInList: false
feature: 
isTop: false
categories: 'Docker'
id: 'docker-notes'
---

## docker 安装

### 环境查看

```shell
# 系统内核3.10以上
[root@VM-0-2-centos ~]# uname -r
3.10.0-1127.19.1.el7.x86_64
```

### 查看系统版本

```shell
# 系统版本
[root@VM-0-2-centos ~]# cat /etc/os-release
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"
```
<!-- more -->
### 卸载旧版本

```shell
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

### 需要的安装包

```shell
yum install -y yum-utils
```

### 设置镜像仓库

```shell
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

### 更新源

```shell
[root@VM-0-2-centos ~]# yum makecache fast
已加载插件：fastestmirror, langpacks
Loading mirror speeds from cached hostfile
epel                                                     | 4.7 kB     00:00
extras                                                   | 2.9 kB     00:00
os                                                       | 3.6 kB     00:00
updates                                                  | 2.9 kB     00:00
元数据缓存已建立
```



### 安装docker相关的软件

```shell
[root@VM-0-2-centos ~]# yum install docker-ce docker-ce-cli containerd.io
已加载插件：fastestmirror, langpacks
Loading mirror speeds from cached hostfile
没有可用软件包 docker-ce。
没有可用软件包 docker-ce-cli。
没有可用软件包 containerd.io。
错误：无须任何处理
[root@VM-0-2-centos ~]# ls
frp0341
[root@VM-0-2-centos ~]# yum-config-manager \
>     --add-repo \
>     https://download.docker.com/linux/centos/docker-ce.repo
已加载插件：fastestmirror, langpacks
adding repo from: https://download.docker.com/linux/centos/docker-ce.repo
grabbing file https://download.docker.com/linux/centos/docker-ce.repo to /etc/yum.repos.d/docker-ce.repo
repo saved to /etc/yum.repos.d/docker-ce.repo
[root@VM-0-2-centos ~]# yum install docker-ce docker-ce-cli containerd.io
已加载插件：fastestmirror, langpacks
Loading mirror speeds from cached hostfile
docker-ce-stable                                         | 3.5 kB     00:00
(1/2): docker-ce-stable/7/x86_64/primary_db                |  58 kB   00:00
(2/2): docker-ce-stable/7/x86_64/updateinfo                |   55 B   00:00
正在解决依赖关系
--> 正在检查事务
---> 软件包 containerd.io.x86_64.0.1.4.4-3.1.el7 将被 安装
--> 正在处理依赖关系 container-selinux >= 2:2.74，它被软件包 containerd.io-1.4.4-3.1.el7.x86_64 需要
---> 软件包 docker-ce.x86_64.3.20.10.5-3.el7 将被 安装
--> 正在处理依赖关系 docker-ce-rootless-extras，它被软件包 3:docker-ce-20.10.5-3.el7.x86_64 需要
--> 正在处理依赖关系 libcgroup，它被软件包 3:docker-ce-20.10.5-3.el7.x86_64 需要
---> 软件包 docker-ce-cli.x86_64.1.20.10.5-3.el7 将被 安装
--> 正在检查事务
---> 软件包 container-selinux.noarch.2.2.119.2-1.911c772.el7_8 将被 安装
--> 正在处理依赖关系 policycoreutils-python，它被软件包 2:container-selinux-2.119.2-1.911c772.el7_8.noarch 需要
---> 软件包 docker-ce-rootless-extras.x86_64.0.20.10.5-3.el7 将被 安装
--> 正在处理依赖关系 fuse-overlayfs >= 0.7，它被软件包 docker-ce-rootless-extras-20.10.5-3.el7.x86_64 需要
--> 正在处理依赖关系 slirp4netns >= 0.4，它被软件包 docker-ce-rootless-extras-20.10.5-3.el7.x86_64 需要
---> 软件包 libcgroup.x86_64.0.0.41-21.el7 将被 安装
--> 正在检查事务
---> 软件包 fuse-overlayfs.x86_64.0.0.7.2-6.el7_8 将被 安装
--> 正在处理依赖关系 libfuse3.so.3(FUSE_3.2)(64bit)，它被软件包 fuse-overlayfs-0.7.2-6.el7_8.x86_64 需要
--> 正在处理依赖关系 libfuse3.so.3(FUSE_3.0)(64bit)，它被软件包 fuse-overlayfs-0.7.2-6.el7_8.x86_64 需要
--> 正在处理依赖关系 libfuse3.so.3()(64bit)，它被软件包 fuse-overlayfs-0.7.2-6.el7_8.x86_64 需要
---> 软件包 policycoreutils-python.x86_64.0.2.5-34.el7 将被 安装
--> 正在处理依赖关系 setools-libs >= 3.3.8-4，它被软件包 policycoreutils-python-2.5-34.el7.x86_64 需要
--> 正在处理依赖关系 libsemanage-python >= 2.5-14，它被软件包 policycoreutils-python-2.5-34.el7.x86_64 需要
--> 正在处理依赖关系 audit-libs-python >= 2.1.3-4，它被软件包 policycoreutils-python-2.5-34.el7.x86_64 需要
--> 正在处理依赖关系 python-IPy，它被软件包 policycoreutils-python-2.5-34.el7.x86_64 需要
--> 正在处理依赖关系 libqpol.so.1(VERS_1.4)(64bit)，它被软件包 policycoreutils-python-2.5-34.el7.x86_64 需要
--> 正在处理依赖关系 libqpol.so.1(VERS_1.2)(64bit)，它被软件包 policycoreutils-python-2.5-34.el7.x86_64 需要
--> 正在处理依赖关系 libapol.so.4(VERS_4.0)(64bit)，它被软件包 policycoreutils-python-2.5-34.el7.x86_64 需要
--> 正在处理依赖关系 checkpolicy，它被软件包 policycoreutils-python-2.5-34.el7.x86_64 需要
--> 正在处理依赖关系 libqpol.so.1()(64bit)，它被软件包 policycoreutils-python-2.5-34.el7.x86_64 需要
--> 正在处理依赖关系 libapol.so.4()(64bit)，它被软件包 policycoreutils-python-2.5-34.el7.x86_64 需要
---> 软件包 slirp4netns.x86_64.0.0.4.3-4.el7_8 将被 安装
--> 正在检查事务
---> 软件包 audit-libs-python.x86_64.0.2.8.5-4.el7 将被 安装
---> 软件包 checkpolicy.x86_64.0.2.5-8.el7 将被 安装
---> 软件包 fuse3-libs.x86_64.0.3.6.1-4.el7 将被 安装
---> 软件包 libsemanage-python.x86_64.0.2.5-14.el7 将被 安装
---> 软件包 python-IPy.noarch.0.0.75-6.el7 将被 安装
---> 软件包 setools-libs.x86_64.0.3.3.8-4.el7 将被 安装
--> 解决依赖关系完成

依赖关系解决

================================================================================
 Package                架构   版本                      源                大小
================================================================================
正在安装:
 containerd.io          x86_64 1.4.4-3.1.el7             docker-ce-stable  33 M
 docker-ce              x86_64 3:20.10.5-3.el7           docker-ce-stable  27 M
 docker-ce-cli          x86_64 1:20.10.5-3.el7           docker-ce-stable  33 M
为依赖而安装:
 audit-libs-python      x86_64 2.8.5-4.el7               os                76 k
 checkpolicy            x86_64 2.5-8.el7                 os               295 k
 container-selinux      noarch 2:2.119.2-1.911c772.el7_8 extras            40 k
 docker-ce-rootless-extras
                        x86_64 20.10.5-3.el7             docker-ce-stable 9.1 M
 fuse-overlayfs         x86_64 0.7.2-6.el7_8             extras            54 k
 fuse3-libs             x86_64 3.6.1-4.el7               extras            82 k
 libcgroup              x86_64 0.41-21.el7               os                66 k
 libsemanage-python     x86_64 2.5-14.el7                os               113 k
 policycoreutils-python x86_64 2.5-34.el7                os               457 k
 python-IPy             noarch 0.75-6.el7                os                32 k
 setools-libs           x86_64 3.3.8-4.el7               os               620 k
 slirp4netns            x86_64 0.4.3-4.el7_8             extras            81 k

事务概要
================================================================================
安装  3 软件包 (+12 依赖软件包)

总下载量：104 M
安装大小：430 M
Is this ok [y/d/N]: y
Downloading packages:
(1/15): container-selinux-2.119.2-1.911c772.el7_8.noarch.r |  40 kB   00:00
(2/15): audit-libs-python-2.8.5-4.el7.x86_64.rpm           |  76 kB   00:00
(3/15): checkpolicy-2.5-8.el7.x86_64.rpm                   | 295 kB   00:00
warning: /var/cache/yum/x86_64/7/docker-ce-stable/packages/docker-ce-20.10.5-3.el7.x86_64.rpm: Header V4 RSA/SHA512 Signature, key ID 621e9f35: NOKEY
docker-ce-20.10.5-3.el7.x86_64.rpm 的公钥尚未安装
(4/15): docker-ce-20.10.5-3.el7.x86_64.rpm                 |  27 MB   02:41
(5/15): containerd.io-1.4.4-3.1.el7.x86_64.rpm             |  33 MB   03:45
(6/15): fuse-overlayfs-0.7.2-6.el7_8.x86_64.rpm            |  54 kB   00:00
(7/15): fuse3-libs-3.6.1-4.el7.x86_64.rpm                  |  82 kB   00:00
(8/15): libcgroup-0.41-21.el7.x86_64.rpm                   |  66 kB   00:00
(9/15): libsemanage-python-2.5-14.el7.x86_64.rpm           | 113 kB   00:00
(10/15): python-IPy-0.75-6.el7.noarch.rpm                  |  32 kB   00:00
(11/15): policycoreutils-python-2.5-34.el7.x86_64.rpm      | 457 kB   00:00
(12/15): slirp4netns-0.4.3-4.el7_8.x86_64.rpm              |  81 kB   00:00
(13/15): setools-libs-3.3.8-4.el7.x86_64.rpm               | 620 kB   00:00
(14/15): docker-ce-rootless-extras-20.10.5-3.el7.x86_64.rp | 9.1 MB   00:44
(15/15): docker-ce-cli-20.10.5-3.el7.x86_64.rpm                                                                                                       |  33 MB  00:05:11
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
总计                                                                                                                                         225 kB/s | 104 MB  00:07:53
从 https://download.docker.com/linux/centos/gpg 检索密钥
导入 GPG key 0x621E9F35:
 用户ID     : "Docker Release (CE rpm) <docker@docker.com>"
 指纹       : 060a 61c5 1b55 8a7f 742b 77aa c52f eb6b 621e 9f35
 来自       : https://download.docker.com/linux/centos/gpg
是否继续？[y/N]：y
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  正在安装    : libcgroup-0.41-21.el7.x86_64                                                                                                                            1/15
  正在安装    : setools-libs-3.3.8-4.el7.x86_64                                                                                                                         2/15
  正在安装    : audit-libs-python-2.8.5-4.el7.x86_64                                                                                                                    3/15
  正在安装    : python-IPy-0.75-6.el7.noarch                                                                                                                            4/15
  正在安装    : slirp4netns-0.4.3-4.el7_8.x86_64                                                                                                                        5/15
  正在安装    : libsemanage-python-2.5-14.el7.x86_64                                                                                                                    6/15
  正在安装    : fuse3-libs-3.6.1-4.el7.x86_64                                                                                                                           7/15
  正在安装    : fuse-overlayfs-0.7.2-6.el7_8.x86_64                                                                                                                     8/15
  正在安装    : checkpolicy-2.5-8.el7.x86_64                                                                                                                            9/15
  正在安装    : policycoreutils-python-2.5-34.el7.x86_64                                                                                                               10/15
  正在安装    : 2:container-selinux-2.119.2-1.911c772.el7_8.noarch                                                                                                     11/15
setsebool:  SELinux is disabled.
  正在安装    : containerd.io-1.4.4-3.1.el7.x86_64                                                                                                                     12/15
  正在安装    : 1:docker-ce-cli-20.10.5-3.el7.x86_64                                                                                                                   13/15
  正在安装    : docker-ce-rootless-extras-20.10.5-3.el7.x86_64                                                                                                         14/15
  正在安装    : 3:docker-ce-20.10.5-3.el7.x86_64                                                                                                                       15/15
  验证中      : 1:docker-ce-cli-20.10.5-3.el7.x86_64                                                                                                                    1/15
  验证中      : checkpolicy-2.5-8.el7.x86_64                                                                                                                            2/15
  验证中      : fuse3-libs-3.6.1-4.el7.x86_64                                                                                                                           3/15
  验证中      : fuse-overlayfs-0.7.2-6.el7_8.x86_64                                                                                                                     4/15
  验证中      : libsemanage-python-2.5-14.el7.x86_64                                                                                                                    5/15
  验证中      : slirp4netns-0.4.3-4.el7_8.x86_64                                                                                                                        6/15
  验证中      : 2:container-selinux-2.119.2-1.911c772.el7_8.noarch                                                                                                      7/15
  验证中      : python-IPy-0.75-6.el7.noarch                                                                                                                            8/15
  验证中      : 3:docker-ce-20.10.5-3.el7.x86_64                                                                                                                        9/15
  验证中      : docker-ce-rootless-extras-20.10.5-3.el7.x86_64                                                                                                         10/15
  验证中      : policycoreutils-python-2.5-34.el7.x86_64                                                                                                               11/15
  验证中      : containerd.io-1.4.4-3.1.el7.x86_64                                                                                                                     12/15
  验证中      : audit-libs-python-2.8.5-4.el7.x86_64                                                                                                                   13/15
  验证中      : setools-libs-3.3.8-4.el7.x86_64                                                                                                                        14/15
  验证中      : libcgroup-0.41-21.el7.x86_64                                                                                                                           15/15

已安装:
  containerd.io.x86_64 0:1.4.4-3.1.el7                      docker-ce.x86_64 3:20.10.5-3.el7                      docker-ce-cli.x86_64 1:20.10.5-3.el7

作为依赖被安装:
  audit-libs-python.x86_64 0:2.8.5-4.el7                      checkpolicy.x86_64 0:2.5-8.el7                    container-selinux.noarch 2:2.119.2-1.911c772.el7_8
  docker-ce-rootless-extras.x86_64 0:20.10.5-3.el7            fuse-overlayfs.x86_64 0:0.7.2-6.el7_8             fuse3-libs.x86_64 0:3.6.1-4.el7
  libcgroup.x86_64 0:0.41-21.el7                              libsemanage-python.x86_64 0:2.5-14.el7            policycoreutils-python.x86_64 0:2.5-34.el7
  python-IPy.noarch 0:0.75-6.el7                              setools-libs.x86_64 0:3.3.8-4.el7                 slirp4netns.x86_64 0:0.4.3-4.el7_8

完毕！
[root@VM-0-2-centos ~]#

```

### 启动docker,查看版本

```shell
[root@VM-0-2-centos ~]# systemctl start docker
[root@VM-0-2-centos ~]# docker version
Client: Docker Engine - Community
 Version:           20.10.5
 API version:       1.41
 Go version:        go1.13.15
 Git commit:        55c4c88
 Built:             Tue Mar  2 20:33:55 2021
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.5
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.13.15
  Git commit:       363e9a8
  Built:            Tue Mar  2 20:32:17 2021
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.4.4
  GitCommit:        05f951a3781f4f2c1911b05e61c160e9c30eaa8e
 runc:
  Version:          1.0.0-rc93
  GitCommit:        12644e614e25b05da6fd08a38ffa0cfe1903fdec
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
[root@VM-0-2-centos ~]#
```

### Hello Word

```shell
[root@VM-0-2-centos ~]# docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
b8dfde127a29: Pull complete
Digest: sha256:308866a43596e83578c7dfa15e27a73011bdd402185a84c5cd7f32a88b501a24
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

### 查看下载的镜像

```shell
[root@VM-0-2-centos ~]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    d1165f221234   2 weeks ago   13.3kB
```

## 卸载docker

```shell
 sudo yum remove docker-ce docker-ce-cli containerd.io

sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

## 腾讯云 更换docker源

```shell
vim /etc/docker/daemon.json
# 输入以下内容,保存.
{
"registry-mirrors": [
 "https://mirror.ccs.tencentyun.com"
]
}
# 重启docker
sudo systemctl restart docker
```

## docker常用命令

```shell
docker version #显示docker版本信息
docker info  #显示docker系统信息,包括镜像和容器信息
docker 命令 --help #显示命令的帮助文档
```

## 镜像命令

### docker images 查看本地主机上的所有镜像

```shell
[root@VM-0-2-centos docker]# docker images
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    d1165f221234   2 weeks ago   13.3kB

[root@VM-0-2-centos docker]# docker images --help

Usage:  docker images [OPTIONS] [REPOSITORY[:TAG]]

List images

Options:
  -a, --all             Show all images (default hides intermediate images)
      --digests         Show digests
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print images using a Go template
      --no-trunc        Don't truncate output
  -q, --quiet           Only show image IDs
```

### docker search 搜索镜像

```shell
[root@VM-0-2-centos docker]# docker search mysql
NAME                              DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql                             MySQL is a widely used, open-source relation…   10634     [OK]
mariadb                           MariaDB Server is a high performing open sou…   3990      [OK]


[root@VM-0-2-centos docker]# docker search --help

Usage:  docker search [OPTIONS] TERM

Search the Docker Hub for images

Options:
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print search using a Go template
      --limit int       Max number of search results (default 25)
      --no-trunc        Don't truncate output
      
      
[root@VM-0-2-centos docker]# docker search mysql --filter=STARS=5000
NAME      DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql     MySQL is a widely used, open-source relation…   10634     [OK]
```



### docker pull 下载镜像

```shell
[root@VM-0-2-centos ~]# docker pull mysql
Using default tag: latest
latest: Pulling from library/mysql
6f28985ad184: Pull complete
e7cd18945cf6: Pull complete
ee91068b9313: Pull complete
b4efa1a4f93b: Pull complete
f220edfa5893: Pull complete
74a27d3460f8: Pull complete
2e11e23b7542: Pull complete
fbce32c99761: Pull complete
08545fb3966f: Extracting   19.5MB/113.1MB
5b9c076841dc: Download complete
ef8b369352ae: Download complete
ebd210f0917d: Download complete
```



### docker rmi 删除镜像

```shell
docker rmi -f 容器id #删除指定容器
docker rmi -f 容器id 容器id 容器id #删除多个容器
docker rmi -f $(docker images -aq) #删除所有容器

[root@VM-0-2-centos ~]# docker rmi -f d1165f221234
Untagged: hello-world:latest
Untagged: hello-world@sha256:308866a43596e83578c7dfa15e27a73011bdd402185a84c5cd7f32a88b501a24
Deleted: sha256:d1165f2212346b2bab48cb01c1e39ee8ad1be46b87873d9ca7a4e434980a7726
```



## 容器命令



### 下载拉取镜像

docker pull centos



### 新建容器并启动

```shell
docker run [可选参数] image

# 参数说明

  --name="Name" #容器名字 tomcat01 tomcat02 ,用来区分容器
-d 						#后台方式运行
-it	使用交互方式运行,进入容器查看内容
-p	指定容器的端口 -p 8080:8080
	-p	ip:主机端口:容器端口
	-p 主机端口:容器端口 (常用)
	-p 容器端口
	容器端口
-P	随机指定端口

[root@VM-0-2-centos ~]# docker run -it centos /bin/bash
[root@053419c0d190 /]# ls
bin  etc   lib	  lost+found  mnt  proc  run   srv  tmp  var
dev  home  lib64  media       opt  root  sbin  sys  usr
[root@053419c0d190 /]# exit
exit

```

### 列出所有运行的容器

```shell
docker ps 
		# 列出当前正在运行的容器
-a	#列出所有容器
-n=? #显示最近创建的容器
-q	#只显示容器的编号

[root@VM-0-2-centos ~]# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@VM-0-2-centos ~]# docker ps -a
CONTAINER ID   IMAGE          COMMAND       CREATED             STATUS                          PORTS     NAMES
053419c0d190   centos         "/bin/bash"   2 minutes ago       Exited (0) About a minute ago             nervous_hugle
d659369cd7c3   d1165f221234   "/hello"      About an hour ago   Exited (0) About an hour ago              zen_stonebraker
[root@VM-0-2-centos ~]#
```

### 退出容器

```shell
exit #直接容器停止并退出
Ctrl+P+Q #容器不停止退出

[root@VM-0-2-centos ~]# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@VM-0-2-centos ~]# docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
centos       latest    300e315adb2f   3 months ago   209MB
[root@VM-0-2-centos ~]# docker run -it centos
[root@e3958c4d528d /]# [root@VM-0-2-centos ~]#  #Ctrl+p+q退出
[root@VM-0-2-centos ~]# docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS          PORTS     NAMES
e3958c4d528d   centos    "/bin/bash"   19 seconds ago   Up 18 seconds             thirsty_solomon
[root@VM-0-2-centos ~]#
```

### 删除容器

```shell
docker rm 容器id #删除指定容器
docker rm -f $(docker ps -aq)	#删除所有容器
docker rm -a -q|xargs docker rm # 删除所有容器

```



### 启动和停止容器的操作

```shell
docker start 容器id #启动容器
docker restart 容器id
docker stop 容器id
docker kill 容器id #强制停止容器

```

## 其它常用命令

### 后台启动容器

```shell
# docker run -d 镜像名

[root@VM-0-2-centos ~]# docker run -d centos
62c46ea2a37054800034585cdc73f4f9e0f980aa8cb3cbaa5c4beca8bb81a365
[root@VM-0-2-centos ~]# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@VM-0-2-centos ~]#

# 常见的坑,docker后台运行,必须要有一个前台进程
# nginx,容器启动后,没提供服务,就会立刻停止
```



### 查看日志

```shell
docker logs -tf --tail num 容器id

-tf #实时显示日志
--tail num #显示日志条数

```



### 查看容器中的进程信息

```shell
top 命令

[root@VM-0-2-centos ~]# docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS          PORTS     NAMES
af1c7b12dd98   centos    "/bin/bash"   38 seconds ago   Up 38 seconds             affectionate_lehmann
[root@VM-0-2-centos ~]# docker top af1c7b12dd98
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                16746               16726               0                   20:58               pts/0               00:00:00            /bin/bash
```



### 查看容器信息

```shell
docker inspect 容器id

[root@VM-0-2-centos ~]# docker inspect af1c7b12dd98
[
    {
        "Id": "af1c7b12dd988e10cd3671d52410dda5fa6b62f30d67d31a430e972b6db095a7",
        "Created": "2021-03-21T12:58:43.09586655Z",
        "Path": "/bin/bash",
        "Args": [],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 16746,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2021-03-21T12:58:43.437721075Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:300e315adb2f96afe5f0b2780b87f28ae95231fe3bdd1e16b9ba606307728f55",
        "ResolvConfPath": "/var/lib/docker/containers/af1c7b12dd988e10cd3671d52410dda5fa6b62f30d67d31a430e972b6db095a7/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/af1c7b12dd988e10cd3671d52410dda5fa6b62f30d67d31a430e972b6db095a7/hostname",
        "HostsPath": "/var/lib/docker/containers/af1c7b12dd988e10cd3671d52410dda5fa6b62f30d67d31a430e972b6db095a7/hosts",
        "LogPath": "/var/lib/docker/containers/af1c7b12dd988e10cd3671d52410dda5fa6b62f30d67d31a430e972b6db095a7/af1c7b12dd988e10cd3671d52410dda5fa6b62f30d67d31a430e972b6db095a7-json.log",
        "Name": "/affectionate_lehmann",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/61625c5c49b478f073624c4be0029218e1deef436a84cfb306c61af3d4f920c4-init/diff:/var/lib/docker/overlay2/410f5daba7036aa601c141f138aed4ad234f406b419f7c01b122ef70ee331c3b/diff",
                "MergedDir": "/var/lib/docker/overlay2/61625c5c49b478f073624c4be0029218e1deef436a84cfb306c61af3d4f920c4/merged",
                "UpperDir": "/var/lib/docker/overlay2/61625c5c49b478f073624c4be0029218e1deef436a84cfb306c61af3d4f920c4/diff",
                "WorkDir": "/var/lib/docker/overlay2/61625c5c49b478f073624c4be0029218e1deef436a84cfb306c61af3d4f920c4/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "af1c7b12dd98",
            "Domainname": "",
            "User": "",
            "AttachStdin": true,
            "AttachStdout": true,
            "AttachStderr": true,
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": true,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/bash"
            ],
            "Image": "centos",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.label-schema.build-date": "20201204",
                "org.label-schema.license": "GPLv2",
                "org.label-schema.name": "CentOS Base Image",
                "org.label-schema.schema-version": "1.0",
                "org.label-schema.vendor": "CentOS"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "fa5bfbe40d49a2a67618cf9d56ada81cf5fed384e547653b569735cbbd6d55cb",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/fa5bfbe40d49",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "77993b5f91d58ab00bd8e7a667feb11af4e5faffa494731d323101199fad3fca",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "416e52c0a778ba926d49e636f6f63da6aa220730c170021e8e8d4f1195c60a87",
                    "EndpointID": "77993b5f91d58ab00bd8e7a667feb11af4e5faffa494731d323101199fad3fca",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]


```



### 进入当前正在运行的容器

```shell
# 容器经常后台运行,如何进入正在运行的容器呢

# 命令
# docker exec -it 容器id bashshell

[root@VM-0-2-centos ~]# docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED         STATUS         PORTS     NAMES
af1c7b12dd98   centos    "/bin/bash"   5 minutes ago   Up 5 minutes             affectionate_lehmann
[root@VM-0-2-centos ~]# docker exec -it af1c7b12dd98 /bin/bash
[root@af1c7b12dd98 /]# ls
bin  etc   lib	  lost+found  mnt  proc  run   srv  tmp  var
dev  home  lib64  media       opt  root  sbin  sys  usr
[root@af1c7b12dd98 /]#

# 方式二
# docker attach 容器ID

[root@VM-0-2-centos ~]# docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS          PORTS     NAMES
af1c7b12dd98   centos    "/bin/bash"   10 minutes ago   Up 10 minutes             affectionate_lehmann
[root@VM-0-2-centos ~]# docker attach af1c7b12dd98
[root@af1c7b12dd98 /]# ls
bin  etc   lib	  lost+found  mnt  proc  run   srv  tmp  var
dev  home  lib64  media       opt  root  sbin  sys  usr
[root@af1c7b12dd98 /]#

# docker exec	#进入新开终端
# docker attach #进入容器运行正在执行的终端,不会新开终端

```



### 从容器内拷贝文件到主机

```shell
docker cp 容器id:容器内路径 目的主机路径

# 示例
[root@VM-0-2-centos ~]# docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS          PORTS     NAMES
af1c7b12dd98   centos    "/bin/bash"   17 minutes ago   Up 17 minutes             affectionate_lehmann
[root@VM-0-2-centos ~]# docker attach af1c7b12dd98
[root@af1c7b12dd98 /]# ls
bin  etc   lib	  lost+found  mnt  proc  run   srv  tmp  var
dev  home  lib64  media       opt  root  sbin  sys  usr
[root@af1c7b12dd98 /]# touch /home/ceshi.txt
# Ctrl+p+q 退出容器
[root@VM-0-2-centos ~]# docker cp af1c7b12dd98:/home/ceshi.txt /usr #拷贝到主机usr目录
[root@VM-0-2-centos ~]# cd /usr #进入主机usr目录
[root@VM-0-2-centos usr]# ls
bin  ceshi.txt  etc  games  include  lib  lib64  libexec  local  sbin  share  src  tmp

```

