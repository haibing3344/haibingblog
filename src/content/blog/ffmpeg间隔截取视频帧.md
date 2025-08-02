---
title: ffmpeg间隔截取视频帧
date: 2020-10-05 16:11:51
tags: [ffmpeg]
published: true
hideInList: false
feature: 
isTop: false
categories: 'FFmpeg'
id: 'ffmpeg-extract-video-frames'
---
    ffmpeg -i abc2.mp4 -vf fps=0.01 a/out%d.png
    
参考:https://blog.csdn.net/zongyue_wang/article/details/81911196

