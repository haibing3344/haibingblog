---
title: 'FFmpeg：视频转码、剪切、合并、播放速调整'
date: 2020-10-05 16:21:51
tags: [ffmpeg]
published: true
hideInList: false
feature: 
isTop: false
categories: 'FFmpeg'
id: 'ffmpeg-video-processing'
---

# 转码
最简单命令如下：
```
ffmpeg -i out.ogv -vcodec h264 out.mp4
ffmpeg -i out.ogv -vcodec mpeg4 out.mp4
ffmpeg -i out.ogv -vcodec libxvid out.mp4
ffmpeg -i out.mp4 -vcodec wmv1 out.wmv
ffmpeg -i out.mp4 -vcodec wmv2 out.wmv
```

<!-- more -->

-i 后面是输入文件名。-vcodec 后面是编码格式，h264 最佳，但 Windows 系统默认不安装。如果是要插入 ppt 的视频，选择 wmv1 或 wmv2 基本上万无一失。

附加选项：-r 指定帧率，-s 指定分辨率，-b 指定比特率；于此同时可以对声道进行转码，-acodec 指定音频编码，-ab 指定音频比特率，-ac 指定声道数，例如

    ffmpeg -i out.ogv -s 640x480 -b 500k -vcodec h264 -r 29.97 -acodec libfaac -ab 48k -ac 2 out.mp4
    
# 剪切
用 -ss 和 -t 选项， 从第 30 秒开始，向后截取 10 秒的视频，并保存：

    ffmpeg -i input.wmv -ss 00:00:30.0 -c copy -t 00:00:10.0 output.wmv
    ffmpeg -i input.wmv -ss 30 -c copy -t 10 output.wmv
达成相同效果，也可以用 -ss 和 -to 选项， 从第 30 秒截取到第 40 秒：

    ffmpeg -i input.wmv -ss 30 -c copy -to 40 output.wmv
值得注意的是，ffmpeg 为了加速，会使用关键帧技术， 所以有时剪切出来的结果在起止时间上未必准确。 通常来说，把 -ss 选项放在 -i 之前，会使用关键帧技术； 把 -ss 选项放在 -i 之后，则不使用关键帧技术。 如果要使用关键帧技术又要保留时间戳，可以加上 -copyts 选项：

    ffmpeg -ss 00:18:54 -i 5G.mp4 -to 01:06:47 -c copy -copyts 5Gcut.mp4
参考：ffmpeg.org

ffmpeg -i 5G.mp4 -ss 00:18:54 -to 01:06:47 -c copy  5Gcut.mp4

# 合并
把两个视频文件合并成一个。

简单地使用 concat demuxer，示例：
```
$ cat mylist.txt
file '/path/to/file1'
file '/path/to/file2'
file '/path/to/file3'

$ ffmpeg -f concat -i mylist.txt -c copy output
```
更多时候，由于输入文件的多样性，需要转成中间格式再合成：
```
ffmpeg -i input1.avi -qscale:v 1 intermediate1.mpg
ffmpeg -i input2.avi -qscale:v 1 intermediate2.mpg
cat intermediate1.mpg intermediate2.mpg > intermediate_all.mpg
ffmpeg -i intermediate_all.mpg -qscale:v 2 output.avi
```
参考：stackoverflow； ffmpeg.org。

# 调整播放速度
加速四倍：

    ffmpeg -i TheOrigin.mp4 -vf  "setpts=0.25*PTS" UpTheOrigin.mp4
四倍慢速：

    ffmpeg -i TheOrigin.mp4 -vf  "setpts=4*PTS" DownTheOrigin.mp4


参考:https://fzheng.me/2016/01/08/ffmpeg/
https://blog.csdn.net/chance_yin/article/details/16118903