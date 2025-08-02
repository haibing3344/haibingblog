---
title: 'psutil/_psutil_common.c:9:20: 致命错误：Python.h：没有那个文件或目录——–的解决记录'
date: 2022-01-07 15:18:56
tags: [Python]
published: true
hideInList: false
feature: 
isTop: false
categories: 'Python'
id: 'psutil-python-h-error-solution'
---
``` shell
[root@VM-16-2-centos ~]# pip3 install psutil
WARNING: Running pip install with root privileges is generally not a good idea. Try `pip3 install --user` instead.
Collecting psutil
  Downloading http://mirrors.tencentyun.com/pypi/packages/47/b6/ea8a7728f096a597f0032564e8013b705aa992a0990becd773dcc4d7b4a7/psutil-5.9.0.tar.gz (478kB)
    100% |████████████████████████████████| 481kB 1.9MB/s
Installing collected packages: psutil
  Running setup.py install for psutil ... error
    Complete output from command /usr/bin/python3 -u -c "import setuptools, tokenize;__file__='/tmp/pip-build-nyy7r089/psutil/setup.py';f=getattr(tokenize, 'open', open)(__file__);code=f.read().replace('\r\n', '\n');f.close();exec(compile(code, __file__, 'exec'))" install --record /tmp/pip-w4nft0_1-record/install-record.txt --single-version-externally-managed --compile:
    running install
    running build
    running build_py
    creating build
    creating build/lib.linux-x86_64-3.6
    creating build/lib.linux-x86_64-3.6/psutil
    copying psutil/_psbsd.py -> build/lib.linux-x86_64-3.6/psutil
    copying psutil/_pslinux.py -> build/lib.linux-x86_64-3.6/psutil
    copying psutil/_common.py -> build/lib.linux-x86_64-3.6/psutil
    copying psutil/_psaix.py -> build/lib.linux-x86_64-3.6/psutil
    copying psutil/_pssunos.py -> build/lib.linux-x86_64-3.6/psutil
    copying psutil/_pswindows.py -> build/lib.linux-x86_64-3.6/psutil
    copying psutil/_psposix.py -> build/lib.linux-x86_64-3.6/psutil
    copying psutil/__init__.py -> build/lib.linux-x86_64-3.6/psutil
    copying psutil/_psosx.py -> build/lib.linux-x86_64-3.6/psutil
    copying psutil/_compat.py -> build/lib.linux-x86_64-3.6/psutil
    creating build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/__main__.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/test_connections.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/test_windows.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/test_testutils.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/test_memleaks.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/test_process.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/test_aix.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/test_sunos.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/test_linux.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/test_posix.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/test_system.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/test_unicode.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/__init__.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/test_misc.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/test_bsd.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/runner.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/test_osx.py -> build/lib.linux-x86_64-3.6/psutil/tests
    copying psutil/tests/test_contracts.py -> build/lib.linux-x86_64-3.6/psutil/tests
    running build_ext
    building 'psutil._psutil_linux' extension
    creating build/temp.linux-x86_64-3.6
    creating build/temp.linux-x86_64-3.6/psutil
    gcc -pthread -Wno-unused-result -Wsign-compare -DNDEBUG -O2 -g -pipe -Wall -Wp,-D_FORTIFY_SOURCE=2 -fexceptions -fstack-protector-strong --param=ssp-buffer-size=4 -grecord-gcc-switches -m64 -mtune=generic -D_GNU_SOURCE -fPIC -fwrapv -fPIC -DPSUTIL_POSIX=1 -DPSUTIL_SIZEOF_PID_T=4 -DPSUTIL_VERSION=590 -DPSUTIL_LINUX=1 -I/usr/include/python3.6m -c psutil/_psutil_common.c -o build/temp.linux-x86_64-3.6/psutil/_psutil_common.o
    psutil/_psutil_common.c:9:20: 致命错误：Python.h：没有那个文件或目录
     #include <Python.h>
                        ^
    编译中断。
    error: command 'gcc' failed with exit status 1

    ----------------------------------------
Command "/usr/bin/python3 -u -c "import setuptools, tokenize;__file__='/tmp/pip-build-nyy7r089/psutil/setup.py';f=getattr(tokenize, 'open', open)(__file__);code=f.read().replace('\r\n', '\n');f.close();exec(compile(code, __file__, 'exec'))" install --record /tmp/pip-w4nft0_1-record/install-record.txt --single-version-externally-managed --compile" failed with error code 1 in /tmp/pip-build-nyy7r089/psutil/
[root@VM-16-2-centos ~]# **yum install python3-devel.x86_64**
已加载插件：fastestmirror, langpacks
Loading mirror speeds from cached hostfile
正在解决依赖关系
--> 正在检查事务
---> 软件包 python3-devel.x86_64.0.3.6.8-18.el7 将被 安装
--> 正在处理依赖关系 python3-rpm-macros，它被软件包 python3-devel-3.6.8-18.el7.x86_64 需要
--> 正在处理依赖关系 python3-rpm-generators，它被软件包 python3-devel-3.6.8-18.el7.x86_64 需要
--> 正在检查事务
---> 软件包 python3-rpm-generators.noarch.0.6-2.el7 将被 安装
---> 软件包 python3-rpm-macros.noarch.0.3-34.el7 将被 安装
--> 解决依赖关系完成

依赖关系解决

=================================================================================
 Package                     架构        版本                 源            大小
=================================================================================
正在安装:
 python3-devel               x86_64      3.6.8-18.el7         updates      217 k
为依赖而安装:
 python3-rpm-generators      noarch      6-2.el7              os            20 k
 python3-rpm-macros          noarch      3-34.el7             os           8.1 k

事务概要
=================================================================================
安装  1 软件包 (+2 依赖软件包)

总下载量：244 k
安装大小：678 k
Is this ok [y/d/N]: y
Downloading packages:
(1/3): python3-rpm-macros-3-34.el7.noarch.rpm             | 8.1 kB  00:00:00
(2/3): python3-rpm-generators-6-2.el7.noarch.rpm          |  20 kB  00:00:00
(3/3): python3-devel-3.6.8-18.el7.x86_64.rpm              | 217 kB  00:00:00
---------------------------------------------------------------------------------
总计                                                387 kB/s | 244 kB  00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  正在安装    : python3-rpm-generators-6-2.el7.noarch                        1/3
  正在安装    : python3-rpm-macros-3-34.el7.noarch                           2/3
  正在安装    : python3-devel-3.6.8-18.el7.x86_64                            3/3
  验证中      : python3-devel-3.6.8-18.el7.x86_64                            1/3
  验证中      : python3-rpm-macros-3-34.el7.noarch                           2/3
  验证中      : python3-rpm-generators-6-2.el7.noarch                        3/3

已安装:
  python3-devel.x86_64 0:3.6.8-18.el7

作为依赖被安装:
  python3-rpm-generators.noarch 0:6-2.el7  python3-rpm-macros.noarch 0:3-34.el7

完毕！
[root@VM-16-2-centos ~]# **pip3 install psutil**
WARNING: Running pip install with root privileges is generally not a good idea. Try `pip3 install --user` instead.
Collecting psutil
  Downloading http://mirrors.tencentyun.com/pypi/packages/47/b6/ea8a7728f096a597f0032564e8013b705aa992a0990becd773dcc4d7b4a7/psutil-5.9.0.tar.gz (478kB)
    100% |████████████████████████████████| 481kB 20.3MB/s
Installing collected packages: psutil
  Running setup.py install for psutil ... done
Successfully installed psutil-5.9.0
[root@VM-16-2-centos ~]#
```