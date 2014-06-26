---
layout: post
title: Android自定义Tab及切换动画
description: 
keywords: Android
---


###Tab形状的drawable文件:###


#####未选中状态--head_nav_corner.xml，色值为#F7F7F7:#####
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


#####选中状态--head_nav_selected_corner.xml，色值为#FF6F84:#####
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


###控件整体布局###



```xml
<FrameLayout
	android:id="@+id/headNav"
	android:layout_width="150dp"
	android:layout_height="30dp"
	android:layout_centerInParent="true"
	android:background="@drawable/head_nav_corner"
	android:padding="2dp"
	android:visibility="gone" >

	<LinearLayout
		android:id="@+id/outNavBg"
		android:layout_width="146dp"
		android:layout_height="26dp"
		android:layout_gravity="left"
		android:orientation="horizontal" >

		<TextView
			android:id="@+id/inNavBg"
			android:layout_width="73dp"
			android:layout_height="26dp"
			android:layout_gravity="center"
			android:background="@drawable/head_nav_selected_corner" />
	</LinearLayout>

	<LinearLayout
		android:layout_width="146dp"
		android:layout_height="26dp"
		android:layout_gravity="left|center_vertical"
		android:orientation="horizontal" >

		<TextView
			android:id="@+id/nav1"
			android:layout_width="0dp"
			android:layout_height="26dp"
			android:layout_weight="1"
			android:gravity="center"
			android:text="最新"
			android:textColor="#fff" />

		<TextView
			android:id="@+id/nav2"
			android:layout_width="0dp"
			android:layout_height="26dp"
			android:layout_weight="1"
			android:gravity="center"
			android:text="热度"
			android:textColor="#FF6F84" />
	</LinearLayout>
</FrameLayout>
```
