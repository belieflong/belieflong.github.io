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
