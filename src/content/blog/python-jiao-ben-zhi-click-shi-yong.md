---
title: 'Python脚本之click使用'
date: 2022-03-29 17:22:56
tags: [Python,shell]
published: true
hideInList: false
feature: 
isTop: false
categories: 'Python'
id: 'python-click-usage'
---

## 安装

```shell
pip3 install click
```

## 快速开始

```py
import click

@click.command()
def hello():
	click.echo('hello word')
	
if __name__ == '__main__':
	hello()
```

## Click定义可选选项Option

```
●在Click中,可以使用dick .option来定义选项
●option 中设置default为默认选项
●option 中设置help为帮助信息
●option 设置type为数据类型
●option 设置hide_input 可以隐藏输入
●option 设置confirmation_prompt可以脸证输入
●option 设置nargs表示接受多个值
```



## Click定义参数Argument

```
●在Click中,可以使用dick.argument来定义参数
●argument 设置nargs 表示接受多个值
●argument 设置type设定格式
●argument 设置type为click File支持对文件操作
```



## Click接受的参数类型

```
●str : 字符串
●int : 数值
●float : 浮点數
●bool : 布尔值
●click.JUID :  UUID值
●clickFile : 文件类型
● click.Path : 文件路径类型
●click.Choice : 可选项类型
●click.IntRange : 数值可选范围
●click.FloatRange : 浮点数可选范围
●click.DateTime : 时间
```



## Click获取用户输入Prompt

```
●Click 提供了dick.prompt要求用户输入

●Click 提供了dlick.confirm要求用户确认
```


<!-- more -->


# 发布cli脚本

以下面脚本为例：命名 `m3p4.py`

```py
import click
import os
# 下载m3u8视频

@click.command()
@click.option('--url', prompt='输入可播放的m3u8地址', help='输入可播放的m3u8地址,将通过ffmpeg下载为mp4视频')
# @click.argument('url', default='https://www.youtube.com/watch?v=dQw4w9WgXcQ',type=str)
@click.argument('videoname', default='video',type=str)
def get_video(url,videoname):
    click.secho(url,fg='green')
    click.secho(videoname,bg='red',fg='white')
    os.system('ffmpeg -i ' + url + ' -c copy ' + videoname + '.mp4')

if __name__ == '__main__':
    get_video()

```



## 编写发布脚本

安装依赖包：

```shell
pip3 install setuptools wheel
```

编写打包脚本

```
from setuptools import setup, find_packages

setup (
	name="m3p4", # 脚本名称
	version="0.0.3", # 版本
	author="Haibing", # 作者名
    author_email="haibing3344@gmail.com", # 作者邮箱
	description="m3u8视频下载", # 脚本描述
	long_description=" #可将m3u8下载为mp4",# 脚本长描述，支持markdown格式
	long_description_content_type= "text/markdown",
	packages=find_packages(),# 自动查找包
	py_modules= ["m3p4"], # 导入的模块
	install_requires= [
		"click" # 安装依赖包
		],
		entry_points={
       'console_scripts':[
           'm3p4=m3p4:get_video' # 命令=模块:函数 指定m3p4脚本里面函数，注意此处模块需与m3p4.py脚本名称一致
        ]
     }
)
```



目录结构：

```shell
m3p4
	- m3p4.py
	- setup.py
```

构建包

```shell
python3 setup.py sdist bdist_wheel

 自动生成dist build 目录
```

本地安装

```shell
python3 setup.py install
```

## 发布cli包

安装依赖twine

```she
pip3 install twine
```

检查包

```shell
twine check dist/*
Checking dist/m3p4-0.0.1-py3-none-any.whl: PASSED
Checking dist/m3p4-0.0.1.tar.gz: PASSED
```

上传包,先到https://www.pypi.org/注册账号(测试包需要到https://test.pypi.org/注册账号)

```shell
(.venv) (base) Pythonlearning % twine upload --repository testpypi dist/* #--repository testpypi 表示上传到测试版本
Uploading distributions to https://test.pypi.org/legacy/
Enter your username: haibing3344
Enter your password:
Uploading m3p4-0.0.1-py3-none-any.whl
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 4.03k/4.03k [00:02<00:00, 1.42kB/s]
Uploading m3p4-0.0.1.tar.gz
100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████| 3.72k/3.72k [00:01<00:00, 2.73kB/s]

View at:
https://test.pypi.org/project/m3p4/0.0.1/
```

上传完成后pypi平台上可查看包：

![](https://haibing.xyz/post-images/1648545847362.png)



## 通过pip3安装脚本

```shel
pip3 install -i https://test.pypi.org/simple/ m3p4==0.0.3
```

## 使用命令

```shell
(.venv) (base) Pythonlearning % m3p4 --help
Usage: m3p4 [OPTIONS] [VIDEONAME]

Options:
  --url TEXT  输入可播放的m3u8地址,将通过ffmpeg下载为mp4视频
  --help      Show this message and exit.
```


