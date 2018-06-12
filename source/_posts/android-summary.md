---
title: Android系统之-简单使用Activity
date: 2017-05-06 17:22:13
categories:
	- Android
tags:
	- 学习总结
---
## Android系统架构

### Linux内核层
> Android 系统是基于Linux 内核的，这一层为Android设备的各种硬件提供了底层的驱动，如显示驱动、音频驱动、照相机驱动、蓝牙驱动、WiFi驱动、电源管理等。
 
### 系统运行库层
> 这一层通过一些C/C++库来为Android系统提供了主要的特性支持。如SQLite、OpenGLES提供3D绘图的支持、Webkit提供了浏览器内核的支持等。

<!--more-->

### 应用框架层
> 主要提供了构建应用程序时可能用到的各种API，Android 自带的一些核心应用就是使用这些API完成的，开发者也可以通过使用这些API开构建自己的应用程序。
 
### 应用层
> 所有安装在手机的应用程序都时属于这一层的。
 
## 使用Activity
### 如何启动Activity
> 四大组件之一，主要用于和用户交互。

**activity->布局->AndroidManifest注册**

``` xml 配置文件FirstActivity
<activity android:name=".FirstActivity">
	<intent-filter>
		<action android:name="android.intent.action.MAIN" />
		<category android:name="android.intent.category.LAUNCHER" />
	</intent-filter>
</activity>
```

#### 显式Intent
``` java 启动Activity
Intent intent = new Intent(FirstActivity.this,SecondActivity.class);
....
startActivityin(intent);
```
**防止重复启动Activity**
``` java
addFlags(Intent.FLAG_ACTIVITY_REORDER_TO_FRONT)
```

#### 隐式Intent

> 指定了一系列更为抽象的action和category等信息

``` xml 配置文件SecondActivity
<activity android:name=".SecondActivity">
	<intent-filter>
		<action android:name="com.example.activity.ACTION_START" />
		<category android:name="android.intent.category.DEFAULT" />
		<指定多个category>
		<data android:scheme="http" />		
	</intent-filter>
</activity>
```
``` java 通过指定action Category启动
Intent intent = new Intent("com.example.activity.ACTION_START");
intent.addCategory("指定多个category");
....
startActivityin(intent);
更多用法：
Intent intent = new Intent(Intent.ACTION_VIEW);
intent.addData(Uri.parse("http://www.baidu.com"));

Intent intent = new Intent(Intent.ACTION_DIAL);
intent.addData(Uri.parse("tel:10086"));
```
> <data>标签还可以配置以下内容
``` xml
android:scheme。 用于指定数据的协议部分，如 http 部分
android:host。 用于指定数据的主机部分，如 www.baidu.com 部分
android:port。 用于指定数据的端口部分，一般紧随在主机名之后
android:path。用于指定主机名和端口之后的部分，如一段网址中跟在域名之后的内容。
android:mimeType。用于指定可以处理的数据类型，允许使用通配符的方式进行指定。
```

#### 向下一个Activity传递数据

``` java 传递值
//传递
intent.putExtra("extra_data,"data"); 
...putXXX();
startActivity(intent);
//获取
Intent intent = getIntent();
String data  = intent.getStringExtra("extra_data"); //获取到dada
...getXXX();
```

#### 返回数据给上一个Activity

``` java 传递返回值
//启动前(第一个activity)
startActivityForResult(intent,1);
//重写方法(onActivityResult)
switch(requestCode){
	case 1:
		if(resultCode == RESULT_OK){
			String returnedData = data.getStringExtra("data_return");
		}
		break;
}

//启动后(返回事件)(第二个activity)
intent.putExtra("data_return","Hello FirstActivity");
setResult(RESULT_OK,intent);
finish();

```

### Activity的生命周期

#### Activity状态

> 每个活动在其生命周期中最多可能会有4种状态

> **运行状态**
位于返回栈的栈顶，这时Activity就处于运行状态。(低内存时系统不愿回收)

> **暂停状态**
不在处于栈顶位置，但仍然看见时，这个Activity就进入了暂停状态。如：对对话框形式的Activity。(低内存时系统不愿回收)

> **停止状态**
不在处于栈顶位置，并且完全不可见时，就进入了暂停状态。系统仍然会为这种Activity保存相应的状态和成员变量，但是这并不是完全可靠的，当其他地方需要内存时，处于停止状态的活动可能会被系统回收。

> **销毁状态**
Activity从返回栈中移除后就变成了销毁状态。

#### Activity的生存期

Activity类中定义了7个回调方法，覆盖了活动生命周期的每一个环节。

{%  img /images/android/activity_recyle.png %}

{%  img /images/android/activity_recyle2.png %}

#### **Activity跳转过程中的区分:**
> AActivity -> BActivity时(假设B全部遮挡住了A):
A:onPause -> B:onCreate -> B:onStart -> B:onResume -> A:onStop
点击返回键时：
B:onPause -> A:onRestart -> A:onStart -> A:onResume -> B:onStop -> B:onDestroy。
目前Activity栈中只有A，在Android中有两个按键在影响Activity生命周期，即Back键和Home键。
*如果按下Back键，系统返回到桌面，并依次执行A:onPause -> A:onStop -> A:onDestroy。*
*如果按下Home键（非长按），系统返回到桌面，并依次执行A:onPause -> A:onStop。*
由此可见，Back键和Home键主要区别在于是否会执行onDestroy。

### Activity被回收

{%  img /images/android/activity_onSave.png %}

## 运行时权限处理
### 运行时判断并让用户选择
``` java
if (ContextCompat.checkSelfPermission(MainActivity.this, Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED) {
	ActivityCompat.requestPermissions(MainActivity.this, new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE}, 1);
}else {
	openAlbum();
}
```
### 启动相册
``` java
//选择照片
private void openAlbum() {
	Intent intent = new Intent("android.intent.action.GET_CONTENT");
	intent.setType("image/*");
	startActivityForResult(intent, CHOOSE_PHOTO);
}
```
<!-- more -->

### 权限请求结果

``` java
@Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
	switch (requestCode){
		case 1:
			if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED){
				openAlbum();
		}else {
			Toast.makeText(this, "您已拒绝权限", Toast.LENGTH_SHORT).show();
		}
			break;
		default:
			break;
	}
}
```