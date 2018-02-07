---
title: Windows转Ubuntu开发(一)
date: 2017-05-06 17:23:25
categories:
	- Android
tags:
	- Linux
---
### 双系统安装(wind10 ubuntu16.04)

> 工具：U盘、ubuntu16.01 镜像、UltraISO
- 具体操作：打开UltraISO->写入硬盘映像->选择好 Ubuntu 镜像和准备写入镜像的 U盘
- 写入方式：USB-ZIP+
- 便捷启动：写入新的硬盘主引导记录 -> USB-ZIP+
- 重启选择U盘启动安装
- 选择与windows 共存

<!-- more -->

### 删除windows安装
> 清除整个磁盘并安装ubuntu

### 搭建开发环境
#### Java、Android搭建

1.下载jdk解压到指定目录。如：(/home/username/Develop/jdk1.8.0_111)
2.配置环境变量 (打开vim /etc/profile)追加以下内容(具体目录根据实际情况而定)
```
export JAVA_HOME=/home/username/Develop/jdk1.8.0_111/
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$CLASSPATH:$JAVA_HOME/lib:$JRE_HOME/lib
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
```
> username为本地用户名

3.执行(source /etc/profile)注销重新登录，让其生效(java -version)检查是否成功
4.安装Eclipse(解压到 /home/username/Develop/eclipse)，在eclipse目录执行 ./eclipse 启动eclipse
5.快捷创建图标(分别执行以下两条命令)
```
ln -s /home/username/Develop/eclipse/eclipse /usr/bin/eclipse
vim /usr/share/applications/eclipse.desktop
```
将下面的代码粘贴到eclipse.desktop里
```
[Desktop Entry]
Type=Application
Name=eclipse
Comment=Eclipse Integrated Development Environment
Exec=/usr/bin/eclipse
Icon=/home/belieflong/Develop/eclipse/icon.xpm
Terminal=false
Categories=Development;IDE;Java;Android;
```
6.搜索eclipse启动即可，并固定到启动器(所有快捷方式都可使用此步骤)
7.安装Android Sudio
8.下载解压Android Studio,进入android-studio/bin 目录,执行 ./sudio.sh 根据提示安装
[点击查看官方Android Studio安装教程](https://developer.android.com/studio/install.html) 
9.安装完成后配置追加Adnroid Studio环境变量，此时全部环境变量如下：
```
export ANDROID_HOME=/home/username/Develop/Android/Sdk/
export ANDROID_STUDIO=/home/username/Develop/android-studio/
export JAVA_HOME=/home/username/Develop/jdk1.8.0_111/
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$CLASSPATH:$JAVA_HOME/lib:$JRE_HOME/lib
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin:$ANDROID_STUDIO/bin:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
```
10.再次执行(source /etc/profile)注销重新登录，让其生效(查看adb)是否成功
11.Android Studio 快捷方式同上。

#### JavaWeb环境

> 工具：JavaEE、MyEclipse、Tomcat、mysql

##### Tomcat
> 官网下载Tomcat解压后进入bin目录
执行 ./startup.sh 开启
执行 ./shutdown.sh 关闭
未完待编写

##### mysql
> 首先卸载自带的
mysql-client-core-5.7
mariadb-client-core-10.0
未完待编写