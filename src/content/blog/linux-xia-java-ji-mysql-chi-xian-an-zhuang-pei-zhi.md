---
title: 'linux下java及mysql离线安装配置'
date: 2022-01-29 16:05:44
tags: [mysql,java]
published: true
hideInList: false
feature: 
isTop: false
categories: 'Linux'
id: 'linux-java-mysql-offline-installation'
---
### 配置Java环境

安装jdk,版本必须为1.8以上。
下载JDK。
创建目录：

```Bash
mkdir /usr/local/java
```


移动jdk到创建的目录

```Bash
cp jdk-8u311-linux-x64.tar.gz /usr/local/java/jdk-8u311-linux-x64.tar.gz
```


解压

```Bash
tar -zxvf jdk-8u311-linux-x64.tar.gz
```


配置环境变量

```Bash
vi /etc/profile
```


文末添加以下内容：

```Bash
export JAVA_HOME=/usr/local/java/jdk1.8.0_311
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
```


保存退出，使profile生效：

```Bash
source /etc/profile
```


验证jdk是否安装成功

```Bash
java -version
```


出现以下提示为成功.
![](https://haibing.xyz/post-images/1643443603687.png)

### 安装mysql

**上传tar包到服务器**


**删除原有的mariadb**

先查看一下是否已经安装了，命令：rpm -qa|grep mariadb

![](https://haibing.xyz/post-images/1643443759765.png)
删除mariadb，命令：rpm -e --nodeps mariadb-libs

**解压缩mysql离线安装包**

```Bash
[root@localhost ~]# cd /home/
[root@localhost home]# ls
cncrypt-admin.jar  jdk-8u311-linux-x64.tar.gz  mysql-5.7.35-1.el7.x86_64.rpm-bundle.tar
[root@localhost home]# tar -xvf mysql-5.7.35-1.el7.x86_64.rpm-bundle.tar
mysql-community-client-5.7.35-1.el7.x86_64.rpm
mysql-community-common-5.7.35-1.el7.x86_64.rpm
mysql-community-devel-5.7.35-1.el7.x86_64.rpm
mysql-community-embedded-5.7.35-1.el7.x86_64.rpm
mysql-community-embedded-compat-5.7.35-1.el7.x86_64.rpm
mysql-community-embedded-devel-5.7.35-1.el7.x86_64.rpm
mysql-community-libs-5.7.35-1.el7.x86_64.rpm
mysql-community-libs-compat-5.7.35-1.el7.x86_64.rpm
mysql-community-server-5.7.35-1.el7.x86_64.rpm
mysql-community-test-5.7.35-1.el7.x86_64.rpm
```


**安装rmp包**

逐个安装，命令如下：

```Bash
rpm -ivh mysql-community-common-5.7.35-1.el7.x86_64.rpm

rpm -ivh mysql-community-libs-5.7.35-1.el7.x86_64.rpm

rpm -ivh mysql-community-client-5.7.35-1.el7.x86_64.rpm

rpm -ivh mysql-community-server-5.7.35-1.el7.x86_64.rpm

```

**启动mysql**

```Bash
systemctl start mysqld
```


**检查是否安装启动成功**

```Bash
systemctl status mysqld
```


**查看默认密码**

```Bash
grep 'temporary password' /var/log/mysqld.log
```


![](https://haibing.xyz/post-images/1643443785773.png)



**登录修改密码**

```Bash
mysql -u root -p
```



因为5.7及以上版本的数据库对密码做了强度要求，默认密码的要求必须是大小写字母数字特殊字母的组合且至少要8位长度

```SQL
alter user user() identified by "Xuwei@123";
```

![](https://haibing.xyz/post-images/1643443817692.png)

**修改密码强度限制**

编辑配置文件：

$ sudo vi /etc/my.cnf

在文件末尾添加以下内容：

plugin-load=validate_password.so

validate-password=OFF

保存退出

二、重启mysqld服务

重启服务，以使得配置文件生效：

$ sudo service mysqld restart
————————————————

**允许远程登录**

```SQL
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'Yuwei@123' WITH GRANT OPTION;
```


**开放远程端口**

```Bash
firewall-cmd --zone=public --add-port=3306/tcp --permanent
```


**重新读取防火墙规则**

```Bash
firewall-cmd --reload
```
### 导入数据库

**命令行导入**

mysql> create database cncrypt;      # 创建数据库 

mysql> use cncrypt;                  # 使用已创建的数据库 
mysql> set names utf8;           # 设置编码

mysql> source /home/cncrypt.sql # 导入备份数据库

