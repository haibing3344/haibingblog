---
title: 'Linux查看当前ssh登录数,linux /centos 查看ssh登陆日志，从SSH登录情况分析服务器安全'
date: 2022-01-29 15:24:52
tags: [linux]
published: true
hideInList: false
feature: 
isTop: false
categories: 'Linux'
id: 'linux-ssh-login-logs-security'
---

# 1.wtmp日志

SSH下直接执行命令 即可查看所有SSH登陆日志 包括IP
last
last -x -F

# 2.查看在线用户情况

(1)w 命令用于显示已经登陆系统的用户列表，并显示用户正在执行的指令。单独执行w命令会显示所有的用户，您也可指定用户名称，仅显示某位用户的相关信息。
```shell
[root@VM-16-2-centos ~]# w
 15:25:37 up 70 days, 17:31,  1 user,  load average: 0.00, 0.01, 0.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
root     pts/0    222.212.98.37    15:16    1.00s  0.02s  0.00s w
[root@VM-16-2-centos ~]#
```

(2)who am i 显示你的出口IP地址，该地址用于SSH连接的源IP
```shell
[root@VM-16-2-centos ~]# who am i
root     pts/0        2022-01-29 15:16 (222.212.98.37)
[root@VM-16-2-centos ~]#
```

# 3.SSH登录日志分析cat /var/log/secure |more

less /var/log/secure|grep 'Accepted'  

less /var/log/auth.log|grep 'Accepted'

检查/var/log目录下的secure(CentOS)或者auth.log(Ubuntu)，如果存在大量异常IP高频率尝试登录，且有成功登录记录(重点查找事发时间段)，在微步在线上查询该登录IP信息，如果为恶意IP且与用户常用IP无关，则很有可能为用户弱口令被成功爆破。

/var/log/其他日志说明：
/var/log/message  一般信息和系统信息
/var/log/secure  登陆信息
/var/log/maillog  mail记录
/var/log/utmp ubuntu登录记录信息？

/var/log/wtmp登陆记录信息(last命令即读取此日志)

## 1、 lastlog 列出所有用户最近登录的信息

lastlog引用的是/var/log/lastlog文件中的信息，包括login-name、port、last login time
```shell
[root@VM-16-2-centos log]# lastlog
用户名           端口     来自             最后登陆时间
root             pts/1    222.212.98.37    六 1月 29 15:36:42 +0800 2022
bin                                        **从未登录过**
daemon                                     **从未登录过**
adm                                        **从未登录过**
lp                                         **从未登录过**
sync                                       **从未登录过**
shutdown                                   **从未登录过**
halt                                       **从未登录过**
mail                                       **从未登录过**
operator                                   **从未登录过**
games                                      **从未登录过**
ftp                                        **从未登录过**
nobody                                     **从未登录过**
systemd-network                            **从未登录过**
dbus                                       **从未登录过**
polkitd                                    **从未登录过**
libstoragemgmt                             **从未登录过**
rpc                                        **从未登录过**
ntp                                        **从未登录过**
abrt                                       **从未登录过**
sshd                                       **从未登录过**
postfix                                    **从未登录过**
chrony                                     **从未登录过**
tcpdump                                    **从未登录过**
syslog                                     **从未登录过**
lighthouse       pts/0    119.29.96.147    五 11月 19 21:44:41 +0800 2021
nginx                                      **从未登录过**
[root@VM-16-2-centos log]#
```
## 2、last  列出当前和曾经登入系统的用户信息

，它默认读取的是/var/log/wtmp文件的信息。输出的内容包括：用户名、终端位置、登录源信息、开始时间、结束时间、持续时间。注意最后一行输出的是wtmp文件起始记录的时间。当然也可以通过last -f参数指定读取文件，可以是/var/log/btmp、/var/run/utmp

语法：last [-R] [-num] [ -n num ] [-adiowx] [ -f file ] [ -t YYYYMMDDHHMMSS ] [name…]  [tty…]

例子：last -x ：显示系统关闭、用户登录和退出的历史

last -i：显示特定ip登录的情况

last -t  20181010120101： 显示20181010120101之前的登录信息

## 3、lastb  列出失败尝试的登录信息

和last命令功能完全相同，只不过它默认读取的是/var/log/btmp文件的信息。当然也可以通过last -f参数指定读取文件，可以是/var/log/btmp、/var/run/utmp