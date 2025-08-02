---
title: ffmpeg 录制直播流信号
date: 2020-10-05 18:21:51
tags: [ffmpeg]
published: true
hideInList: false
feature: 
isTop: false
categories: 'FFmpeg'
id: 'ffmpeg-record-live-stream'
---
``` bash
ffmpeg -i https://mobilelive-cnc-cdn.ysp.cctv.cn/ysp/E2B44C65BEA385FD28B7651233347CD4D5AC888EEDA8B8B9EE86E5C53F6B33D108F7A7B40E235942544582364B9D7B8BEF3CCF73410685F199705CCF16C2E645D6C69E08A33FDE8F87B2E4C4737A6DD9126ED29E6B703C7E152D8ECCDFF65D1F/2001891501_hd.m3u8 -c:v copy -c:a copy -bsf:a aac_adtstoasc abc.mp4
```

这条命令会持续不断地抓取网络视频流，然后写入abc.mp4文件，直到你按下键盘上的“Q”键才停止。如果你就想录制一小段时间（比如60秒），可以在-i参数前加-t参数来控制，如下：

    ffmpeg -t 60 -i http://60.199.188.151/HLS/WG_ETTV-N/index.m3u8 abc.mp4

参考:https://blog.csdn.net/happydeer/article/details/52735694

## ffmpeg 安装

参考:https://blog.csdn.net/u013314786/article/details/89682800

cd /usr/bin

ln -s /root/ffmpeg-4.2.2-amd64-static/ffmpeg ffmpeg

ln -s /root/ffmpeg-4.2.2-amd64-static/ffprobe ffprobe

    nohup ffmpeg -i https://mobilelive-cnc-cdn.ysp.cctv.cn/ysp/E2B44C65BEA385FD28B7651233347CD4D5AC888EEDA8B8B9EE86E5C53F6B33D108F7A7B40E235942544582364B9D7B8BEF3CCF73410685F199705CCF16C2E645D6C69E08A33FDE8F87B2E4C4737A6DD9126ED29E6B703C7E152D8ECCDFF65D1F/2001891501_hd.m3u8 -c:v copy -c:a copy -bsf:a aac_adtstoasc abc.mp4 &