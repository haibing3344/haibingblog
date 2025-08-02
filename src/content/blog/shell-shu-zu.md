---
title: 'shell数组'
date: 2022-02-13 23:10:02
tags: [linux,shell]
published: true
hideInList: false
feature: 
isTop: false
categories: 'Linux'
id: 'shell-arrays'
---
## 1. 数组

### 1.1 什么是shell数组


shell的数组就是把有限个元素(变量或字符内容)用一个名字命名，然后用编号对他们进行区分的元素集合。这个名字就称为数组名，用于区分不同内容的编号就称为数组下标。组成数组的各个元素(变量)称为数组的元素，有时也称为下标变量。下标默认是从0开始。

### 1.2 数组的分类



```shell
普通数组：只能使用整数 作为数组索引 
关联数组：可以使用字符串 作为数组索引
```

### 1.3 数组的赋值方式

数组赋值方式： 一次赋多个值
 数组名=(多个变量值)



```bash
[root@apple scripts]# array=(1 2 3 4 5)
[root@apple scripts]# echo ${array[0]}
1
[root@apple scripts]# echo ${array[1]}
2
[root@apple scripts]# echo ${array[2]}
3
[root@apple scripts]# echo ${array[3]}
4
[root@apple scripts]# echo ${array[4]}
5
```

数组赋值方式:针对每个索引进行赋值
 数组名[索引]=变量值



```shell
[root@apple ~]# arraytest[0]=beijing
[root@apple ~]# arraytest[1]=shenzhen
[root@apple ~]# arraytest[2]=shanghai
```

数组赋值方式:第三种



```bash
[root@apple scripts]#array=([1]=one [2]=two [3]=three) 
[root@apple scripts]# array=([1]=one [2]=two [3]=three) 
[root@apple scripts]# echo ${array[*]}
one two three
[root@apple scripts]# echo ${array[0]}

[root@apple scripts]# echo ${array[1]}
one 
```

数组赋值方式：动态赋值



```bash
array=($(ls))
array=(`ls`)
```

覆盖



```ruby
[root@apple scripts]# array=([1]=one [2]=two [3]=three) 
[root@apple scripts]# echo ${array[*]}
one two three
[root@apple scripts]# echo ${array[0]}

[root@apple scripts]# echo ${array[1]}
one
[root@oshell scripts]# array[0]=a;array[1]=b;array[2]=c
[root@apple scripts]# echo ${array[*]}
a b c three
```

### 1.4 查看数组



```bash
查看数组所有元素
[root@applescripts]# echo ${array[*]}
1 2 3 4 5
[root@apple scripts]# echo ${array[@]}
1 2 3 4 5
统计元素的个数
[root@apple scripts]# echo ${#array[@]} 
5
[root@apple scripts]# echo ${#array[*]}
5
获取数组元素的索引 
[root@apple scripts]# echo ${!array[@]}
0 1 2 3 10
```

### 1.5 查看数组的赋值结果



```shell
[root@apple ~]#  declare –a     查看普通数组
[root@apple ~]#  declare –A     查看关联数组
```

### 1.6 关联数组

关联数组可以用字符串当索引

##### 1.6.1定义关联数组



```shell
[root@apple ~]# declare -A array_1
[root@apple ~]# declare -A array_2
```

##### 1.6.2 关联数组赋值

关联数组的赋值方式一，针对每个索引进行赋值



```shell
#数组名[索引]=变量值
[root@apple ~]# declare -A array_1
[root@apple ~]# declare -A array_2
[root@apple ~]# array_1[index1]=beijing
[root@apple ~]# array_1[index2]=shenzhen
[root@apple ~]# array_1[index3]=shanghai
```

关联数组的赋值方式二，一次赋多个值



```shell
[root@apple ~]#  array_2=([index1]=beijing [index2]=shenzhen [index3]=shanghai)
```

访问数据元素



```shell
[root@apple ~]# echo ${array_2[index2]}
shenzhen
[root@apple ~]# echo ${array_2[@]}     
beijing shenzhen shanghai
[root@apple ~]# echo ${!array_2[@]} 
index1 index2 index3
```

1.7 例题
 输出123456两种方法



```bash
array=(1 2 3 4 5)
for n in ${array[*]}
do
    echo $n
done

echo --------------
for((i=0;i<${#array[*]};i++))
do
    echo ${array[i]}
done  
```

利用bash for循环打印下面这句话中字母数不大于6的单词（某企业面试真题）。
 I am English teacher welcome to English training class
 要求用定义数组完成



```bash
array=(I am English teacher welcome to English training c
lass)
echo "第一种"
for n in ${array[*]}
do
    if [ ${#n} -lt 7 ]
    then
        echo $n
    else
        continue
    fi
done

echo "第二种"
for((i=0;i<${#array[*]};i++))
do
   [ ${#array[i]} -le 6 ]&&
       echo ${array[i]}
done
```



```bash
方法3：通过awk循环实现。
[root@apple scripts]# chars="I am English teacher welcome to English training class"
[root@apple scripts]# echo $chars|awk '{for(i=1;i<=NF;i++) if(length($i)<=6)print $i}' 
```

### 1.8 遍历数组

范例1



```bash
已知文件里有名字对应的性别 请统计性别出现的总次数
let array_pa[m]++
let array_pa[f]++
let array_pa[x]++
let array_pa[m]++
其实就是对相同索引进行计数

[root@apple ~]# cat sex.txt 
gs m
eg m
mz f
wr m
zs f
ls m
[root@apple ~]# cat count_sex.sh 
#!/bin/sh
declare -A sex
while read line
do
        type=$(echo $line|awk '{print $2}')
        let sex[$type]++
done<sex.txt
#遍历数组
for i in ${!sex[*]}
do
        echo $i 共有${sex[$i]}个
done
```

范例2



```bash
统计nginx日志IP访问次数
[root@apple ~]# cat nginx_count.sh 
#!/bin/sh
declare -A array_nginx
while read line
do
        type=$(echo $line|awk '{print $1}')
        let array_nginx[$type]++

done</var/log/nginx/access.log

for i in ${!array_nginx[*]}
do
      
    echo "IP是 $i 共出现了${array_nginx[$i]}次"
done
```

案例3



```bash
统计tcp状态信息
[root@apple ~]# cat nginx_status.sh 
#!/bin/sh
declare -A array_nginx
type=`ss -an|grep 80|awk '{print $2}'`
for i in $type
do
        let     array_nginx[$i]++
done
for n in ${!array_nginx[*]}
do
        echo $n ${array_nginx[$n]}
done
```

