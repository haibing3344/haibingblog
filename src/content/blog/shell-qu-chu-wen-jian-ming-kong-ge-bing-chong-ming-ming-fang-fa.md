---
title: 'shell去除文件名空格并重命名方法'
date: 2022-03-02 15:17:03
tags: [shell,linux]
published: true
hideInList: false
feature: 
isTop: false
categories: 'Linux'
id: 'shell-remove-filename-spaces'
---

```shell
#!/bin/bash
#去除空格
for loop in `ls -1 | tr ' '  '#'`
 do  
    mv  "`echo $loop | sed 's/#/ /g' `"  "`echo $loop |sed 's/#//g' `"  2> /dev/null 
done
```
> 首先利用ls -1（不是字母l，是数字1），将单个文件放在一行，然后利用替换，就文件名中的空格替换为#（具体自己看情况）,下面就是利用一些替换将文件名给替换回来，不过需要记住，含有空格的文件名需要使用引号括起来，最终就可以替换当前目录下的所有文件名中的空格


```shell
#!/bin/bash
#重命名
for i in `ls`;do mv $i ${i#*-};done
```
```shell
${i#*-}表示字符串截取，去掉都一个「-」左边的字符
# ## 删除左边，保留右边 echo ${var##*字符} 两个#表示最后一个字符
% %% 删除右边，保留左边 echo ${var%字符*} 两个%表示最后一个字符
```
