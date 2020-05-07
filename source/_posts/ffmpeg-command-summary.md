---
title: FFmpeg命令总结
date: 2018-03-23 15:45:04
categories:
	- FFmpeg
tags:
	- 学习总结
---

**flv转换为mp4文件**
``` sh
ffmpeg -i wang_yi.flv -y -vcodec copy -acodec copy wang_yi_copy.mp4
```
<!-- more -->

**ffmpeg如何控制profile&level**
``` sh
ffmpeg -i input.mp4 -profile:v baseline -level 3.0 output.mp4

ffmpeg -i input.mp4 -profile:v main -level 4.2 output.mp4

ffmpeg -i input.mp4 -profile:v high -level 5.1 output.mp4
```

**设置输出视频的分辨率**
```
ffmpeg -i input_file -vcodec h264 -s 1280x720 output_file  
```

**flv转换为mp4文件**
``` sh
ffmpeg.exe -i source.mp4 -c:v libx264 -ar 22050 -crf 28 destinationfile.flv
ffmpeg.exe -i source.mp4 -c:v libx264 destination.flv
```
-crf 控制转码后视频的质量，质量越高，文件也就越大。
此值的范围是 0 到 51：0 表示高清无损；23 是默认值（如果没有指定此参数）；51 虽然文件最小，但效果是最差的。
值越小，质量越高，但文件也越大，建议的值范围是 18 到 28。而值 18 是视觉上看起来无损或接近无损的，当然不代表是数据（技术上）的转码无损。
-ar 采样率 设定声音采样率，PSP只认24000 

**提取YUV数据**
``` sh
ffmpeg -i input.mp4 -an -c:v rawvideo -pix_fmt yuv420p out.yuv
```

**提取PCM数据**
``` sh
ffmpeg -i input.mp4 -vn -ar 44100 -ac2 -f s16le out.pcm
```

**播放pcm**
``` sh
ffplay input.pcm -f s16le -channels 2 -ar 44100
```

**播放yuv**
``` sh
ffplay -f rawvideo -pixel_format yuv420p -s 640*360 file_640_360.yuv
```

**按键小技巧**
``` html
按w显示音频的波形图、左右键快进快退10s
按s进入frame-step模式，按s键一次就会播放下一帧图像
```

**列出电脑的设备**
``` sh
ffmpeg -list_devices true -f dshow -i dummy
```

**测试摄像头**
``` sh
ffplay -f dshow -i video="HP HD Camera" //通过list_devices打印出来的名称
```

**查询摄像头信息**
``` sh
ffmpeg -list_options true -f dshow -i video="HP HD Camera"
```

**本地摄像头推流**
``` sh
ffmpeg -f dshow -i video="USB 视频设备" -vcodec libx264 -preset:v ultrafast -tune:v zerolatency -f flv rtmp://xxx
```

**本地推送文件指定编码格式**
``` sh
ffmpeg -re -stream_loop -1 -i file.flv -vcodec libx264 -acodec aac -f flv -y rtmp://xxx
```
