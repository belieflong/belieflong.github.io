---
title: Android随笔总结
date: 2017-05-06 17:22:44
categories:
	- Android
tags:
	- 学习总结
---
**防止重复启动Activity**
``` java
addFlags(Intent.FLAG_ACTIVITY_REORDER_TO_FRONT)
```
**Gson简单使用**
Java对象转化Json数据
``` java
Gson gson = new Gson();
gson.toJson(Object);
```

<!--more-->

Json数据转化Java对象
网络访问成功返回数据的方法
``` java
public void onResponse(String response) {  
    //成功获取网络json数据  
     Child2 child2 = gson.fromJson(response, Child2.class);
}  
List<Child2> child2List = gson.fromJson(response, new TypeToken<List<Child2>>(){}.getType());
```
>未完待更新