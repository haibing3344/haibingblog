---
title: 'centos 添加开机自启脚本'
date: 2022-03-22 17:52:10
tags: [shell,linux]
published: true
hideInList: false
feature: 
isTop: false
categories: 'Linux'
id: 'centos-autostart-script'
---
以脚本autostart.sh为例：
```shell
#!/bin/bash
#description:开机自启脚本
/usr/local/tomcat/bin/startup.sh  #启动tomcat
```

1、赋予脚本可执行权限（/opt/script/autostart.sh是你的脚本路径）
```shell
chmod +x /opt/script/autostart.sh
```

2、打开/etc/rc.d/rc.local或/etc/rc.local文件，在末尾增加如下内容
```shell
cat /etc/rc.d/rc.local
#!/bin/bash
# THIS FILE IS ADDED FOR COMPATIBILITY PURPOSES
#
# It is highly advisable to create own systemd services or udev rules
# to run scripts during boot instead of using this file.
#
# In contrast to previous versions due to parallel execution during boot
# this script will NOT be run after all other services.
#
# Please note that you must run 'chmod +x /etc/rc.d/rc.local' to ensure
# that this script will be executed during boot.

touch /var/lock/subsys/local
/usr/local/qcloud/irq/net_smp_affinity.sh >/tmp/net_affinity.log 2>&1
/usr/local/qcloud/cpuidle/cpuidle_support.sh &> /tmp/cpuidle_support.log
/usr/local/qcloud/rps/set_rps.sh >/tmp/setRps.log 2>&1
/usr/local/qcloud/irq/virtio_blk_smp_affinity.sh > /tmp/virtio_blk_affinity.log 2>&1
/usr/local/qcloud/gpu/nv_gpu_conf.sh >/tmp/nv_gpu_conf.log 2>&1
/opt/script/autostart.sh >/root/frp_0.34.1_linux_amd64/frps.log 2>&1 # 自启动脚本

```

3、在centos7中，/etc/rc.d/rc.local的权限被降低了，所以需要执行如下命令赋予其可执行权限
```shell
chmod +x /etc/rc.d/rc.local
```

<!-- more -->
