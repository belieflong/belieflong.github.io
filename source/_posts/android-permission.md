---
title: Android运行时权限处理
date: 2017-05-06 17:20:53
categories:
	- Android
tags: 
	- Android权限
---

## 运行时权限的处理
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