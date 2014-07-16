---
layout: post
title: Android实现service定时启动及开机启动
description: 实现服务的开机启动，用于监听推送等
keywords: Android, Boot
---


####定义Service继承自BroadcastReceiver####
+ 在Manifest文件中定义Intent-Filter，添加Action如下
		```xml
			<action android:name="android.intent.action.BOOT_COMPLETED" />
		```
+ 重写OnReceive函数，
