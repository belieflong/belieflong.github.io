---
title: adb工具常用的命令
date: 2018-12-04 04:03:00
categories:
	- Android
tags:
	- 学习总结
---

### 启动和停止服务
``` shell
adb start-server
adb kill-server
```
### 查看APK包名
``` shell
aapt dump badging <file_path.apk> 
aapt工具在 android-sdk\build-tools对应的目录下
```
<!--more-->
### 启动
``` shell
am start -n 包名/.LauncherActicity //清单文件中配置的
```
### 安装以及卸载
``` shell
adb install xxx.apk
adb uninstall 包名
adb shell pm uninstall -k 包名 保留用户数据
```
### 通过IP地址连接设备
``` shell
adb connect ip地址 
```
### 关闭连接
``` shell
adb disconnect
``` 
### 查看已经连接的设备
``` shell
adb devices
```
### 进入shell模式 
``` shell
adb shell
adb -s 10.1.3.150 shell 指定具体设备
```
### 查看应用版本
``` shell
adb shell dumpsys package com.examle.xx
```
### 输出安装包的APK路径
``` shell
adb shell pm path <PACKAGE>
```
### 删除与包相关的所有数据：清除数据和缓存
``` shell
adb shell pm clear <PACKAGE>
```
### 获取系统版本
``` shell
adb shell getprop ro.build.version.release
```
### 获取系统api版本
``` shell
adb shell getprop ro.build.version.sdk
```
### 获取相关制造商信息
``` shell
adb shell getprop | grep "model\|version.sdk\|manufacturer\|hardware\|platform\|revision\|serialno\|product.name\|brand"
```
### 获取设备名称 
``` shell
cat /system/build.prop
```
### 推送文件到系统
``` shell
adb push d:/key.xml /sdcard
```
### 拉取文件到当前目录
``` shell
adb pull /sdcard .
```
### 查看内存
``` shell
adb shell procrank
```
### 使文件系统可读写
``` shell
adb shell mount -o remount,rw /system
adb remount
或
adb shell
# mount 查看挂载
找到挂载的名称
/emmc@android /system ext4 rw,seclabel,relatime,noauto_da_alloc,commit=1,data=ordered 0 0
# mount -o rw,remount -t ext4 /emmc@android system/
```
### 写日志
``` shell
adb logcat -s TAG > xx.log      //指定TAG相关的日志写入文件
adb logcat | grep PID > xx.log  //根据PID将日志写入文件
adb logcat -c                   //清空日志
adb logcat > xx.log             //开始文件通过Ctrl C 关掉即停止
adb logcat -d > xx.log          //将缓存的日志输出到文件
```
### 帮助
``` shell
adb logcat --help
```