---
title: 'ffmpeg推流'
date: 2020-08-23 16:21:51
tags: [ffmpeg]
published: true
hideInList: false
feature: 
isTop: false
categories: 'FFmpeg'
id: 'ffmpeg-streaming'
---
    ffmpeg -re -i [视频地址or直播流地址] -c copy -f flv [推流地址]