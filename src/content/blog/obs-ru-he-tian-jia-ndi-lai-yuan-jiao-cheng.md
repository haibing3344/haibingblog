---
title: 'OBS如何添加NDI来源教程'
date: 2020-10-10 16:59:43
tags: []
published: true
hideInList: false
feature: 
isTop: false
categories: '视频'
id: 'obs-add-ndi-source-tutorial'
---
1、正确安装OBS软件。

2、打开OBS软件，在“来源”的空闲区域点击右键，或是点击左下角位置“+”，会弹出“添加”选项，可以显示当前可添加的视频源列表，比如图像、场景、媒体源等。如果没有显示“NDI来源”一项，说明需要安装obs-ndi插件。

![](https://images5doc.oss-cn-beijing.aliyuncs.com/images/20201010171547.png)

3、打开网站链接：<https://github.com/Palakis/obs-ndi/releases>，点击对应安装包将obs-ndi插件下载至本地，然后进行安装。

![obs-ru-he-tian-jia-ndi-lai-yuan-jiao-cheng-2020-10-10-20201010171837](https://images5doc.oss-cn-beijing.aliyuncs.com/images/obs-ru-he-tian-jia-ndi-lai-yuan-jiao-cheng-2020-10-10-20201010171837.png)

这里以WIN64位为例：

解压NDI插件包后，将data文件夹下obs-plugins文件夹里的文件全部复制到OBS的同名文件夹下，将obs-plugins文件夹下64bits文件夹里的文件全部复制到OBS的同名文件夹下。启动OBS会提示缺少NewTek NDI的ndi-runtime-4.5.1-Windows.exe程序。点击链接<https://ndi.palakis.fr/runtime/ndi-runtime-4.5.1-Windows.exe>下载安装。

安装之后在“来源”里面添加可以看到“NDI来源”。（添加插件之后，可能需要重启程序或是电脑才能生效）

4、点击“NDI来源”，针对新建NDI源设置名称，然后点击“确定”。

![obs-ru-he-tian-jia-ndi-lai-yuan-jiao-cheng-2020-10-10-20201010171918](https://images5doc.oss-cn-beijing.aliyuncs.com/images/obs-ru-he-tian-jia-ndi-lai-yuan-jiao-cheng-2020-10-10-20201010171918.png)

5、在弹出的“属性”对话框，点击“来源名称”右侧下拉箭头，可以显示当前发现的NDI视频源，选择一个你想要添加的视频源，其他参数可选择默认，然后点击“确定”。

![obs-ru-he-tian-jia-ndi-lai-yuan-jiao-cheng-2020-10-10-20201010171942](https://images5doc.oss-cn-beijing.aliyuncs.com/images/obs-ru-he-tian-jia-ndi-lai-yuan-jiao-cheng-2020-10-10-20201010171942.png)

6、NDI源将添加至“来源”区域，并在“预览”区域实时播放。

![obs-ru-he-tian-jia-ndi-lai-yuan-jiao-cheng-2020-10-10-20201010171959](https://images5doc.oss-cn-beijing.aliyuncs.com/images/obs-ru-he-tian-jia-ndi-lai-yuan-jiao-cheng-2020-10-10-20201010171959.png)