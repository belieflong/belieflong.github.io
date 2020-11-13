---
title: 编译webrtc windows源码
date: 2020-10-18 13:20:010
categories:
	- WebRTC
tags:
	- webrtc
---

# 搭建webrtc windows编译环境
## 安装depot_tools
### 下载后将其解压到某个目录
https://storage.googleapis.com/chrome-infra/depot_tools.zip
<!-- more -->
### 配置环境变量
新建DEPOT_TOOLS_WIN_TOOLCHAIN 设置为0
Path中添加depot_tools路径
配置好以后执行一次 gclient （为了安装相关依赖工具）
## 下载源代码
``` sh
fetch --nohooks webrtc
gclient sync
```
# 编译
## 提前安装好vs2017
目前好像只能在线安装 默认勾线安装windows sdk
记得安装Debugging Tools for Windows，可通过控制面板-程序 右击 Windows Software Development Kit 选择修改 勾选安装
注意最新的webrtc源码依赖于最新的windows sdk，参照下边的链接安装最新的sdk
## 编译命令
``` sh
gn gen --ide=vs out/Default --args="is_debug=false"
ninja -C out/Default
```
## 编译成功
``` sh
ninja -C out/Default
ninja: Entering directory `out/Default'
[5224/5224] STAMP obj/default.stamp
```
## 报windows sdk版本的问题时下载最新的sdk安装
``` sh
https://developer.microsoft.com/zh-cn/windows/downloads/windows-10-sdk/
```