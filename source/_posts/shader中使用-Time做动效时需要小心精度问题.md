---
title: shader中使用_Time做动效时需要小心精度问题
index_img: /posts_img/unity_tips.jpg
banner_img: /posts_img/shader中使用-Time做动效时需要小心精度问题/banner.webp
categories:
  - Unity
  - 小贴士
tags:
  - Unity
  - tips
  - 小贴士
  - shader
  - _Time
date: 2022-12-03 22:20:16
---
### 1.关于Unity Shader中时间相关的相关变量
***
#### 1.Unity中设置了4个时间相关的变量
![图1：shader中可用的时间变量](unity_time.png)<br>
注意：这里的t,是指场景（Scene）加载以来的时间，那么在场景加载时间比较长之后，就可能出现浮点精度不足的情况。

#### 2.关于基于时间变化实现的动效卡顿的问题
基于时间_Time在shader实现的动效，可能运行时间久了，会出现画面一卡一顿的问题。大部分情况下，是因为时间精度不够用了。而这种情况，经常是在PC上难以复现，在手机（特别是低端手机）上容易出现。从经验上说，_Time.x 比 _Time.y "精度更高"。这里说精度更高可能不太准确，但我不知道用什么术语来描述。举个例子，假设现在只用4位（xxxx）来表示一个数，那么，如果是用t来填充，填充到1000秒的时候，小数位就没了，只能一秒一秒的递增了，但是，如果用t/20来填充，那么可以到20000（20000/20=1000）秒的时候，小数位才表达不了。由于小数位越多的时候，动效看上去才会越顺畅。所以如果shader中用的是_Time.y 或者_Time.z甚至是Time.w做的动效，在手机上出现游戏运行一段时间，动效看起来卡顿，但游戏画面本身不怎么掉帧，试试改_Time.x，可能会出现奇迹~
