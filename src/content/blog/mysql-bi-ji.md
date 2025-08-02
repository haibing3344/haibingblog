---
title: 'Mysql笔记'
date: 2021-04-05 02:09:51
tags: []
published: true
hideInList: false
feature: 
isTop: false
categories: '数据库'
id: 'mysql-notes'
---

## 安装



```shell
wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
rpm -ivh mysql-community-release-el7-5.noarch.rpm
yum update
yum install mysql-server

```

## 启动

权限设置：

```
chown mysql:mysql -R /var/lib/mysql
```

初始化 MySQL：

```
mysqld --initialize
```

启动 MySQL：

```
systemctl start mysqld
```

查看 MySQL 运行状态：

```
systemctl status mysqld
```

<!-- more -->

## 报错解决

### 启动失败,查看日志:

```shell
cat /var/log/mysqld.log
```

在mysql错误日志里出现：The innodb_system data file ‘ibdata1’ must be writable

字面意思：’ibdata1必须可写 
那么解决方案自然是更改对应权限

通过yum安装的话， 
5.7版本以前是 
chmod -R 777 /usr/local/mysql/data/ 
5.7版本以后是 
chmod -R 777 /var/lib/mysql

如果不是通过yum安装的话： 
find / -name ibdata1 
找到对应目录更改权限~



### 登录报错:Access denied for user 'root'@'localhost' (using password: NO)

修改配置文件,在[mysqld]后添加skip-grant-tables（使用 set password for设置密码无效，且此后登录无需键入密码）

skip-grant-tables   #在my.ini，[mysqld]下添加一行，使其登录时跳过权限检查.

```shell
[root@VM-0-2-centos ~]# whereis my.cnf
my: /etc/my.cnf
[root@VM-0-2-centos ~]# vi /etc/my.cnf
```

[mysqld]
skip-grant-tables

![](https://haibing.xyz/post-images/1617559929715.png)

重启mysql.

```shell
systemctl restart mysqld
```

