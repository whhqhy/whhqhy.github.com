---
title: android学习
date: 2016-10-17 09:08:16
categories:
tags: [android]
keywords:
description: 控件大小获取
---

有时候我们需要获得控件的大小,但是在Activity的onCreate()生命周期方法中调用getWidth()和getHeight()方法并不能获得控件的宽和高，因为此时我们的界面并未被绘制完成。不过我们却可以在onWindowFocusChanged(boolean hasFocus)这个方法中获得控件的大小。
```
public void onWindowFocusChanged(boolean hasFocus) {
    super.onWindowFocusChanged(hasFocus);
    int height = headerTextView2.getHeight();
    int width = headerTextView2.getWidth();
}
```
当前窗口的Activity在获得或者失去焦点的时候就会调用这个方法,它是这个Activity是否对用户可见的最好标志。
那么对于Fragment又该怎么办呢?Fragment并未提供类似onWindowFocusChanged的方法。这时我们就需要用到ViewTreeObserver了。
```
ViewTreeObserver observer = headerTextView.getViewTreeObserver();
observer.addOnPreDrawListener(new ViewTreeObserver.OnPreDrawListener() {
    public boolean onPreDraw() {
        if (!isMeasured) {
            int layoutHeight = headerTextView.getMeasuredHeight();
            isMeasured = true;
        }
        return true;
    }
});
```

 解释：重写view中的onMeasure()方法可以知道，这个方法是用来计算view的宽度和高度，所以只要重写onMeasure()以 后的方法，然后再那个方法里面获取view的大小就行了。通过测试，一个Activity中，各种方法调用顺序如下：

其调用顺序为Activity.oncreate()→Activity.onResume()→
→TestImageView.onMeasure()→TestImageView.onLayout()→onGlobalLayoutListener()→
→Activity.onWidnowFocusChanged()→.....→
→TextImageView.onDraw()

引用自：[调用顺序](http://www.xuebuyuan.com/1587193.html)
