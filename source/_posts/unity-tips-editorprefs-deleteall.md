---
title: 谨慎使用EditorPrefs.DeleteAll()
date: 2022-10-27 23:50:56
index_img: /posts_img/unity_tips.jpg
banner_img: /posts_img/unity-tips-editorprefs-deleteall/banner.jpg
categories:
- Unity
- 小贴士
tags: 
- Unity
- tips
- 小贴士
---

在使用EditorPrefs相关API时需要谨慎，特别是`EditorPrefs.DeleteAll()`<br>
因为Unity编辑器的本地配置信息就保存在`EditorPrefs`里<br>
在不知情的情况下调用了`EditorPrefs.DeleteAll()`API，可能会出现一些意想不到的问题。<br>
比如：<br>
C#不自动编译了！<br>
自宝义的SDK路径丢失了！<br>

总之，有点抓狂！<br>
