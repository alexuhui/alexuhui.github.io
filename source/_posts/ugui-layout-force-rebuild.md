---
title: 强制重建UGUI布局
index_img: /posts_img/unity_tips.jpg
banner_img: /posts_img/ugui-layout-force-rebuild/banner.webp
categories:
  - Unity
  - 小贴士
  - UGUI
tags:
  - Unity
  - tips
  - 小贴士
  - UGUI
date: 2022-12-19 22:12:28
---
### 1.什么是重建
***
重建就是ui元素发生改变后，重新构建UI网格。UGUI的布局组件在内容发生改变后，调用`SetDirty()`，通过`LayoutRebuilder`类的静态方法`MarkLayoutForRebuild(RectTransform rect)`，标记需要重建的`RectTransform`。标记对象最终会保存在`CanvasUpdateRegistry`的重建队列`m_LayoutRebuildQueue`里，并在`PerformUpdate（）`函数里完成重建。
### 2.为什么要强制重建
***
有的时候，自己的逻辑里面可能会需要使用ui的大小或者位置数据去手动计算UI布局，这个时候，就有可能由于UGUI布局刷新不及时，导致我们拿到的实际上是刷新之前的数据，从而导致错误。比如，自己实现的虚拟列表，需要根据列表的每个Item的Size计算Item的坐标。如果每个item的大小不一样，而且大小根据item要显示的内容动态改变。这个时候，如果不能保证自己的计算逻辑在系统重建之后进行，就拿错误的参数进行计算从而导致异常。
### 3.怎么强制重建
***
调用`LayoutRebuilder`类的静态方法`ForceRebuildLayoutImmediate(RectTransform layoutRoot)`即可！