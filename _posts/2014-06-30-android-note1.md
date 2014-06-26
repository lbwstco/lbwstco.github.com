---
layout: post
title: Android自定义Tab及切换动画
description: 
keywords: Android
---


####构造单一Tab的drawable:

#####未选中状态，色值为#F7F7F7:
```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android" >
	<solid android:color="#F7F7F7" />    
	<corners android:topLeftRadius="10dp"   
		android:topRightRadius="10dp"    
		android:bottomRightRadius="10dp"   
		android:bottomLeftRadius="10dp"/>
</shape>
```
#####选中状态，色值为#FF6F84:
```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android" >
	<solid android:color="#FF6F84" />    
	<corners android:topLeftRadius="10dp"   
		android:topRightRadius="10dp"    
		android:bottomRightRadius="10dp"   
		android:bottomLeftRadius="10dp"/>
</shape>
```
