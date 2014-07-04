---
layout: post
title: Android TranlateAnimation动画循环播放
description: 
keywords: TranslateAnimation, Repeat
---


####实现控件上下循环移动####


```Java
private void arrowAnimation() {
	TranslateAnimation translateAnimation = new TranslateAnimation(0, 0, 0, 3.0f);
	translateAnimation.setDuration(150);
	translateAnimation.setFillAfter(true);
	translateAnimation.setFillEnabled(true);
	translateAnimation.setRepeatCount(Animation.INFINITE);
	translateAnimation.setRepeatMode(Animation.REVERSE);
	widget.startAnimation(translateAnimation);
}
```
