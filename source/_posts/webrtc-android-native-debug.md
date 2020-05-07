---
title: Ubuntu下断点调试webrtc android native层源码
date: 2019-11-03 12:06:010
categories:
	- WebRTC
tags:
	- webrtc
---

### 环境搭建ubuntu
需要将webrtc android源码整体编译完成后进行
1、拷贝webrtc/src/third_party下的Android SDK和NDK文件夹到某个目录
2、配置环境变量
``` sh
export ANDROID_HOME=~/android/android_sdk
export ANDROID_NDK_HOME=~/android/android_sdk/ndk-bundle
export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$ANDROID_NDK_HOME
```
<!-- more -->
3、安装Android Studio（记得安装64位环境下的依赖库）
下载官方的as安装包，以及安装依赖，并启动
``` sh
sudo apt-get install libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1 libbz2-1.0:i386
```
``` sh 
cd android-studio/bin && ./studio.sh
```
3、安装SDK相关工具
Build Tools、Cmake、LLDB （可通过as的sdk管理界面安装）
4、安装golang-go（编译报错 : go: not found）
``` sh
sudo apt install golang-go
```
### 编译webrtc as工程代码
1、下载webrtc android_gradle工程，将android_gradle工程放到源码/src/sdk目录下
``` sh
 https://github.com/HackWebRTC/webrtc/tree/hack_webrtc/sdk/android_gradle
```
2、修改gradle.properties中的相关路径问题。如：webrtc_repo、python、compile_native_code=true、protoc (/src/out/Debug/clang_x64/protoc) ，使用Android Studio打开
#### 修改apprtc配置文件中版本号
1、注释掉源码中src/examples/androidapp/AndroidManifest.xml中的版本号
#### 执行sync碰到的报错问题
as中执行sync时，生成相关文件路径为：/src/out/android_studio/gen
根据实际报错内容进行解决，比如M77分支碰到的问题：
1、找不到头文件：根据报错内容在源码中找到RefCounted.java文件，定位到void release() 方法，添加@CalledByNative 
2、注释掉webrtc.build中"--input_file sdk/android/api/org/webrtc/CandidatePairChangeEvent.java "文件等，input_file文件在源码中已经不存在了，所以要根据实际情况修改否则会报错。
3、删除out/android_studio/gen重新sync；sync期间出现一个文件生成有问题，则接下来的文件也将无法生成
#### build期间报错问题
出现该问题一般都是文件不存在或者路径问题，需要根据当前源代码
1、检查/src/sdk/android_gradle/webrtc/third_party下报错模块的CMakeLists.txt里相关文件的路径是否正确
2、例如：编译时报 src/sdk/android_gradle/webrtc/third_party/protobuf中找不到generated_enum_util.cc文件，则需要根据源码中 src/third_party对应模块中的xxx.gni文件所包含的源文件路径，对android_gradle工程下对应的CMakeLists.txt进行修改
3、例如：M77分支修改了as工程中 libvpx、protobuf模块下的CMakeLists.txt
### 成功跑起来后就可以断点调试了
{% img /images/webrtc/webrtc-debug-screenshot.png %}