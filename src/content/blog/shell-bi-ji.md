---
title: 'shell笔记'
date: 2022-02-16 10:14:54
tags: [shell,linux]
published: true
hideInList: false
feature: 
isTop: false
categories: 'Linux'
id: 'shell-notes'
---


## 创建及执行

#!/bin/bash  #约定标记
echo "Hello World !"



shell执行：

chmod +x shell.sh

./shell.sh



## shell变量

变量名= "变量值"

```shell
for file in `ls .`;do
	echo "$file"
done
# 列出当前目录下的文件名
```

只读变量

```shell
 readonly 变量名
```

删除变量 

```
unset 变量名
```

字符串

```shell
单双引号区别
字符串拼接
your_name="runoob"
# 使用双引号拼接
greeting="hello, "$your_name" !"
greeting_1="hello, ${your_name} !"
echo $greeting  $greeting_1
# 使用单引号拼接
greeting_2='hello, '$your_name' !'
greeting_3='hello, ${your_name} !'
echo $greeting_2  $greeting_3
```

获取字符串长度

```shell
string="abcd"
echo ${#string} #输出 4
```

字符串截取

```shell
# ## 删除左边，保留右边 echo ${var##*字符} 两个#表示最后一个字符
% %% 删除右边，保留左边 echo ${var%字符*} 两个%表示最后一个字符

```

<!-- more -->

单行注释

```shell
# 注释
```

多行注释

```shell
:<<EOF
注释内容
EOF
```

## shell传参

```shell
./test.sh 参数1 参数2 参数3 ...

$0 执行的文件名及路径
$1 $2 $3 第1、2、3个参数
$* 显示传递的所有参数
$@ 分别显示传递的所有参数

echo "-- \$* 演示 ---"
for i in "$*"; do
    echo $i
done

echo "-- \$@ 演示 ---"
for i in "$@"; do
    echo $i
done

$ chmod +x test.sh 
$ ./test.sh 1 2 3
-- $* 演示 ---
1 2 3
-- $@ 演示 ---
1
2
3

```



## shell数组

定义数组

```shell
array_name=(value1 value2 ... valuen)
```

读取数组

```shell
${array_name[index]}
```

获取数组所有元素

```shell
${array_name[@]}
${array_name[*]}
```

获取数组长度

```shell
${#array_name[@]}
${#array_name[*]}
```



例：

```shell
#!/bin/bash
test_array = (a b c d)

echo "第3个元素是：${test_array[2]}"
echo "所有元素：${test_array[*]}"
echo "数组长度：${#test_array[@]}"

#输出结果
第3个元素是：c
所有元素：a b c d
数组长度：4
```



## shell运算符

- 算数运算符

```shell
#!/bin/bash


a=10
b=10

val=`expr $a + $b` # expr 用``包含
echo "a + b : $val"
if [[ $a == $b ]] # 条件表达式要放在方括号之间，并且要有空格。
then
	echo "a等于b"
fi

# 使用 [[ ... ]] 条件判断结构，而不是 [ ... ]，能够防止脚本中的许多逻辑错误。比如，&&、||、< 和 > 操作符能够正常存在于 [[ ]] 条件判断结构中，但是如果出现在 [ ] 结构中的话，会报错。
```



- 关系运算符

```shell
-eq	检测两个数是否相等，相等返回 true。	[ $a -eq $b ] 返回 false。
-ne	检测两个数是否不相等，不相等返回 true。	[ $a -ne $b ] 返回 true。
-gt	检测左边的数是否大于右边的，如果是，则返回 true。	[ $a -gt $b ] 返回 false。
-lt	检测左边的数是否小于右边的，如果是，则返回 true。	[ $a -lt $b ] 返回 true。
-ge	检测左边的数是否大于等于右边的，如果是，则返回 true。	[ $a -ge $b ] 返回 false。
-le	检测左边的数是否小于等于右边的，如果是，则返回 true。	[ $a -le $b ] 返回 true。
```



- 布尔运算符

```shell
!	非运算，表达式为 true 则返回 false，否则返回 true。	[ ! false ] 返回 true。
-o	或运算，有一个表达式为 true 则返回 true。	[ $a -lt 20 -o $b -gt 100 ] 返回 true。
-a	与运算，两个表达式都为 true 才返回 true。	[ $a -lt 20 -a $b -gt 100 ] 返回 false。
```



- 字符串运算符

```shell
=	检测两个字符串是否相等，相等返回 true。	[ $a = $b ] 返回 false。
!=	检测两个字符串是否不相等，不相等返回 true。	[ $a != $b ] 返回 true。
-z	检测字符串长度是否为0，为0返回 true。	[ -z $a ] 返回 false。
-n	检测字符串长度是否不为 0，不为 0 返回 true。	[ -n "$a" ] 返回 true。
$	检测字符串是否为空，不为空返回 true。	[ $a ] 返回 true。
```



- 文件测试运算符

```shell
-b file	检测文件是否是块设备文件，如果是，则返回 true。	[ -b $file ] 返回 false。
-c file	检测文件是否是字符设备文件，如果是，则返回 true。	[ -c $file ] 返回 false。
-d file	检测文件是否是目录，如果是，则返回 true。	[ -d $file ] 返回 false。
-f file	检测文件是否是普通文件（既不是目录，也不是设备文件），如果是，则返回 true。	[ -f $file ] 返回 true。
-g file	检测文件是否设置了 SGID 位，如果是，则返回 true。	[ -g $file ] 返回 false。
-k file	检测文件是否设置了粘着位(Sticky Bit)，如果是，则返回 true。	[ -k $file ] 返回 false。
-p file	检测文件是否是有名管道，如果是，则返回 true。	[ -p $file ] 返回 false。
-u file	检测文件是否设置了 SUID 位，如果是，则返回 true。	[ -u $file ] 返回 false。
-r file	检测文件是否可读，如果是，则返回 true。	[ -r $file ] 返回 true。
-w file	检测文件是否可写，如果是，则返回 true。	[ -w $file ] 返回 true。
-x file	检测文件是否可执行，如果是，则返回 true。	[ -x $file ] 返回 true。
-s file	检测文件是否为空（文件大小是否大于0），不为空返回 true。	[ -s $file ] 返回 true。
-e file	检测文件（包括目录）是否存在，如果是，则返回 true。	[ -e $file ] 返回 true。
```



## echo 命令

```shell
#!/bin/sh
echo -e "OK! \c" # -e 开启转义 \c 不换行
echo "It is a test"

输出：OK!It is a test
```



```shell
实例, 文件 test.sh:

read -p "请输入一段文字:" -n 6 -t 5 -s password
echo -e "\npassword is $password"参数说明：
 -p 输入提示文字
 -n 输入字符长度限制(达到6位，自动结束)
 -t 输入限时
 -s 隐藏输入内容
 
 ./test.sh
 请输入一段文字:
 password is abcdef
```



## frintf命令

```
printf  format-string  [arguments...]
```

```shell
$  printf "%d %-2s %c %-3.2f\n" 1111 "abc" "def" 3.1413
1111 ab d  3.14

%-2s 指一个宽度为 2 个字符（- 表示左对齐，没有则表示右对齐），任何字符都会被显示在 2 个字符宽的字符内，如果不足则自动以空格填充，超过也会将内容全部显示出来。

%-3.2f 指格式化为小数，其中 .2 指保留2位小数
```



**%s %c %d %f** 都是格式替代符，**％s** 输出一个字符串，**％d** 整型输出，**％c** 输出一个字符，**％f** 输出实数，以小数形式输出。



## shell test命令

数值测试

```shell
-eq	等于则为真
-ne	不等于则为真
-gt	大于则为真
-ge	大于等于则为真
-lt	小于则为真
-le	小于等于则为真
```



字符串测试

```shell
=	等于则为真
!=	不相等则为真
-z 字符串	字符串的长度为零则为真
-n 字符串	字符串的长度不为零则为真
```



文件测试

```shell
-e 文件名	如果文件存在则为真
-r 文件名	如果文件存在且可读则为真
-w 文件名	如果文件存在且可写则为真
-x 文件名	如果文件存在且可执行则为真
-s 文件名	如果文件存在且至少有一个字符则为真
-d 文件名	如果文件存在且为目录则为真
-f 文件名	如果文件存在且为普通文件则为真
-c 文件名	如果文件存在且为字符型特殊文件则为真
-b 文件名	如果文件存在且为块特殊文件则为真

-O 判断对象是否存在，并且属于当前用户
-G 判断对象是否存在，并且属于当前用户组
-nt 判断file1是否比file2新  [ "/data/file1" -nt "/data/file2" ]
-ot 判断file1是否比file2旧  [ "/data/file1" -ot "/data/file2" ]
```

```shell
另外，Shell 还提供了与( -a )、或( -o )、非( ! )三个逻辑操作符用于将测试条件连接起来，其优先级为： ! 最高， -a 次之， -o 最低。例如：

cd /bin
if test -e ./notFile -o -e ./bash
then
    echo '至少有一个文件存在!'
else
    echo '两个文件都不存在'
fi
```



## 流程控制

if else

```shell
if condition1
then
	command1
	command2
elif condition2
then
	command3
else
	commadn4
fi
```

For 循环

```shell
for loop in 1 2 3
do
	echo "$loop"
done
```

While语句

```shell
while condition
do
	command
done
```

无限循环

```shell
while :
do
    command
done

或者

for (( ; ; ))

```

until循环

```shell
#!/bin/bash

a=0

until [ ! $a -lt 10 ]
do
   echo $a
   a=`expr $a + 1`
done
```

Case...esac

```shell
case 值 in
模式1)	
	command
	;;	#;;表示break
模式2)
	command
	;;
esac
```

例

```shell
echo '输入 1 到 4 之间的数字:'
echo '你输入的数字为:'
read aNum
case $aNum in
    1)  echo '你选择了 1'
    ;;
    2)  echo '你选择了 2'
    ;;
    3)  echo '你选择了 3'
    ;;
    4)  echo '你选择了 4'
    ;;
    *)  echo '你没有输入 1 到 4 之间的数字'
    ;;
esac
```



调出循环

break

continue

## shell函数

```shell
function funname [()]

{

    action;

    [return int;]

}
```

例：

```shell
#!/bin/bash
function demofun1(){
	echo "shell函数demo"
	return 0
}
demofun1
```



## shell输入/输出重定向

```shell
command > file	将输出重定向到 file。
command < file	将输入重定向到 file。
command >> file	将输出以追加的方式重定向到 file。
n > file	将文件描述符为 n 的文件重定向到 file。
n >> file	将文件描述符为 n 的文件以追加的方式重定向到 file。
n >& m	将输出文件 m 和 n 合并。
n <& m	将输入文件 m 和 n 合并。
<< tag	将开始标记 tag 和结束标记 tag 之间的内容作为输入。
```



```shell
ls >> ls.txt
cat ls.txt

command 2>>file #报错追加到文件末尾

command >> file 2>&1

文件描述符 0 通常是标准输入（STDIN），1 是标准输出（STDOUT），2 是标准错误输出（STDERR）。
```

```shell
command > /dev/null # /dev/null 是一个特殊的文件，写入到它的内容都会被丢弃

command > /dev/null 2>&1  # 禁止输出
```

输入重定向

```shell
command1 < file1
```

Here Document :它的作用是将两个 delimiter 之间的内容(document) 作为输入传递给 command。

```shell
command << delimiter
    document
delimiter

例：

```



## shell文件包含

```shell
. filename   # 注意点号(.)和文件名中间有一空格

或

source filename
```

例：

```
#!/bin/bash
# shell1.sh
name=(1 2 3 4 5) #定义那么数组
```

```shell
#!/bin/bash
# shell2.sh
. ./shell1.sh # 引用shell1.sh
for i in ${name[*]};do # 循环显示数组元素
	echo "$i"
done

[root@VM-16-2-centos ~]# ./shell2.sh
1
2
3
4
5
```


