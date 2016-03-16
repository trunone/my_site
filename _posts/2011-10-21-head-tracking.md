---
layout: post
title: 頭部追縱(Head Tracking)簡介
date: '2011-10-21T22:33:00.000+08:00'
author: Chih-En Wu
tags:
- FreeTrack
- Flight Simulator
modified_time: '2011-10-24T17:24:53.906+08:00'
thumbnail: https://img.youtube.com/vi/BduSDvUU6MY/default.jpg
blogger_id: tag:blogger.com,1999:blog-6518933078301809282.post-6075066285260759179
blogger_orig_url: http://trunone.blogspot.com/2011/10/head-tracking.html
---

以前常在電影裡看到一個很酷的畫面，
就是主角的頭移到哪，螢幕上的畫面就會跟著跑到哪
但其實現在很容易可以做到了，主要有兩種。

一種是臉部追縱，
顧名思義就是透找出你臉部所朝向的位置來決定移動的方向。
在硬體上很方便準備，只要有一台足夠解析度的 Webcam 和一張正常人的臉(誤)

軟體方面較成熟的是用 FaceTraceNoIR 與遊戲連接配合 faceAPI 做臉部辨識，
但缺點是你得要有一顆夠快的 CPU，因為要從一張出片中找出人臉是要一定計算量的。
何況是每秒要處理30張以上，或者是用兩台電腦，一台玩遊戲，一台做追縱也行。
我希望我的CPU資源不要浪費在頭部追縱上，因此就不用這個方法，下面是faceAPI官方的介紹影片：

<div class="separator" style="clear: both; text-align: center;"><iframe width="420" height="315" src="http://www.youtube.com/embed/BduSDvUU6MY" frameborder="0" allowfullscreen></iframe></div>
另一種方法就是使用紅外線，這是什麼意思呢？
其實一樣是使用攝影機，但比較特別是我們要讓它只接收紅外線。

接下來再想辦法在頭上弄出幾個紅外線發射源。
這裡又分兩種方式，反射式與發射式。

反射式是在鏡頭旁裝上 IR LED 照到你的頭部，
然後在你的頭上黏一些可以反射的東西像是鋁鉑紙之類的。
好處是頭上不用裝電池盒或接一條電線，但是要改造 Webcam 較多，而且要多比較多顆的 IR LED

那發射式就是直接在頭上裝 IR LED，好處是光源穩定 IR LED 最多四顆就非常足夠了。

![6-DOF](https://upload.wikimedia.org/wikipedia/commons/f/fa/6DOF_en.jpg)
如果你是正常人的話，上面這張圖就你的頭能移動的六個自由度(6 Degree of Freedom)。
那麼要是只使用一顆 IR LED，電腦就只能算出你的兩個自由度(2DoF) 也就是Yaw和Pitch

那使用三顆IR LED就能算出六個自由度，而四顆的話是可以減少不確定的方向。
但是其實只要用三顆品質好一點一 IR LED 就沒什麼問題了。

Reference:

* <a href="http://www.seeingmachines.com/product/faceapi/">faceAPI</a>
* <a href="http://www.free-track.net/english/">FreeTrack</a>
