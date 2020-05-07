---
title: OWT Server 环境搭建
date: 2020-04-05 09:03:00
categories:
	- WebRTC
tags:
	- owt
---

### 下载源码
下载指定的版本
``` sh
wget https://github.com/open-webrtc-toolkit/owt-server/archive/v4.3.zip -O owt-server-4.3.zip
unzip owt-server-4.3.zip
```
官方的仓库
``` sh
git clone https://github.com/open-webrtc-toolkit/owt-server.git
```
<!--more-->
### 安装依赖
``` sh
cd owt-server && ./scripts/installDepsUnattended.sh
```
### 编译native模块
``` sh
./script/pack.js –t mcu –check
```
注意：GitHub上-t的参数是all，但如果服务器不支持硬件加速，会出错，所以在此我们使用mcu参数
此命令会下载相关的依赖并编译
### 下载及编译app
``` sh
git cline https://github.com/open-webrtc-toolkit/owt-client-javascript.git
```
npm install grunt-cli -g 此步骤可以省略，安装依赖时已经安装上了
若提示node不存在时，可以使用如下方式：
nvm -v、nvm ls、nvm use node版本号
``` sh
cd owt-client-javascript/scripts && npm install && grunt
```
如果想要生成debug的demo，则把grunt换成grunt debug，此时在dist目录下会生成sdk-debug目的。
### 打包
``` sh
./scripts/pack.js -t all -f -a -s ~/owt-client-javascript-4.3/dist/samples/conference
```
运行的时候需要owt-client-javascript这个demo
### 配置 owt-server (在dist目录下)
1、打开webrtc_agent/agent.toml目录，设置你服务器的公网IP，修改 [webrtc] 部分的 network_interfaces
添加{name = "enp0s3", replaced_ip_address = "本地ip地址"}
2、编辑 portal/portal.toml：修改 [portal] 部分里的 ip_address 为服务器公网 IP 地址
修改 ip_address = "本地ip地址"
### 初始化
``` sh
cd owt-server/dist/ && ./bin/init-all.sh
```
注意，此时会生成superID及superKey，后面登录console的时候需要使用到，并询问你是否初始化rabbitMQ及mongoDB，输入NO即可。
如果点了YES，在后面启动模块的时候会报错（删除当前dist目录，再执行一次打包的步骤）
### 启动所有模块服务：
``` sh
./bin/start-all.sh
./bin/stop-all.sh
```
### 启动测试页面
``` txt
https://localhost:3004
https://localhost:3004/forward=true
```
### 验证后台服务
console可以用来创建service及创建房间，输入(使用superId及superKey登录) https://localhost:3300/console
### 注意事项
(1).下载时网络需要代理
(2).执行init脚本时，选择No；登陆后台时，使用init生成的key登录
(3).可以手动指定node（nvm use node版本号）或配置环境变量
(4).修改server源码中的installCommonDeps.sh脚本，否则出现openssl-1.0.2下载失败的问题
``` sh
将http://www.openssl.org/source/openssl-${SSL_VERSION}.tar.gz
修改为http://www.openssl.org/source/old/1.0.2/openssl-${SSL_VERSION}.tar.gz可正常下载
```