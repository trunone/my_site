---
layout: post
title: FreeTrack硬體篇
date: '2011-10-25T23:37:00.000+08:00'
author: Chih-En Wu
tags:
- FreeTrack
- Flight Simulator
modified_time: '2011-10-25T23:40:53.029+08:00'
thumbnail: http://2.bp.blogspot.com/-LUxf-0aMkwA/TqV_NewlynI/AAAAAAAAA8s/jeloz9p7QaM/s72-c/wiimote.jpg
blogger_id: tag:blogger.com,1999:blog-6518933078301809282.post-6692978391477094486
blogger_orig_url: http://trunone.blogspot.com/2011/10/freetrack.html
---

Webcam
----------

如果要使用反射式的方法的話 那就要買有照明功能的 再把上面的LED全換成IR LED
或是自己在一般Webcam旁邊黏一圈IR LED 不管哪種都很麻煩 所以我用發射式來實做

在Webcam規格的選擇上 FPS要越高越好 最少要有30才不會有延遲感
這裡說的FPS可不是CS那種，而是Frame per Second，也就是每秒Webcam可以錄到的影格數
解析度則有640x480就夠了 再高就沒有意義 這點現在大部分的Webcam都能達成

由於幾乎所有的Webcam都會在鏡頭上加一層可以濾掉紅外線的濾鏡 要想辦法拿掉它
因為我們需要的就是紅外線 可不能把它濾掉
不過每個Webcam的做法不同 有的只是一片黏在鏡頭後面 這就很容易拿下來
但有的是直接鍍在鏡頭上 這就很麻煩 要用工具把它磨掉 直到看見透明的鏡片

光讓紅外線能清楚的看到還不夠 接下來還要濾掉可見光 讓Webcam只看到IR LED的光
有幾種東西可以使用 3.5"磁片的碟片、曝光後的底片或是相機用的濾光鏡
前兩著是比較便宜也易取得的 相機的濾光鐿可能就比較貴
取得後把它們黏在鏡頭前面就可以了

![Wiimote]({{ site.url }}/images/wiimote.jpg)

但我使用的是Wiimote 它前面的攝影機就是為紅外線量身定做的 所以不用做任何改造
而且有高達100的FPS 而雖然它的解析度只有128x96 但它有良好的內插演算法
所以對光點移動的位置還是能知道得很精準

連接電腦的方法是使用藍芽 因此沒有內建藍芽的電腦需要再買一個藍芽接收器
不過因為Wiimote是用電池 所以有使用時間的限制
現在好像也有可以對Wiimote持續供電的變壓器模組

但要注意的是要使用原廠的Wiimote才能追縱多達四個點 大部分的副廠都只有二點 除非你只打算用一個IR LED

頭戴式紅外線發射器
-------------------

到電子材料行採構IR LED前 要注意幾個重要的規格
如果是使用Wiimote的話 IR LED得要買波長850nm以上的 不然Wiimote會看不到
還有發射角度越大越好 免得頭轉動角度太大就接收不到紅外線了
再來是一般運作時的順向電壓(Forward Voltage)和順向電流(Forward Current)必需要確定清楚
還有它們的最大可承受值 這樣才能知道要用多大的限流電阻

電源的部分可以選擇電池、USB電源、變壓器
除非你不常用 不然的話不建議使用電池 而且一個電池盒吊在頭上也有點重
USB電源可以找不要的USB連接線使用 變壓器也可以直接找不要的 除非都沒有才去買

[這裡](http://www.free-track.net/english/hardware/calcled)有FreeTrack官網提供的工具來計算要用的限流電阻和連接方式
在選電源的部分如果選非正規電源(Unregulated power supply) 它計算的時候會把你的電壓加30%
因為它覺得一般變壓器實際的電壓都會 比標示的高
但我用三用電表量我的變壓器 是有高一點 但還不到10% 因此我還是選正規電源來計算(Regulated power supply)
所以最好是手邊有工具可以實際量測你所用的電源的電壓

那麼計算完成後就可以買電阻了 計算完成的畫面還有提供電阻的色來辨視電阻的大小
如果可以的話IR LED和電阻可以多買幾個 如果燒壞了可以備用

![]({{ site.url }}/images/tracker-circuit.jpg)

如果有麵包板的話可以先在上面測試 IR LED長的那端是正極 建議電阻接在第一顆IR LED前 再與電源的正極相接
人眼看不到紅外線(如果你看得到的話……) 不過相機可以 檢查一下有沒有正常發亮
正常的話就把它們焊起來吧 再找個衣架或是什麼東西做成下圖(左)的形狀 把做好的電路綁上去
之後會需要在FreeTrack裡輸入一些長度資料 下圖(右)

|:-:|:-:|:-:|
<img src="{{ site.url }}/images/tracker.jpg" style="width: 300px;" />||![]({{ site.url }}/images/tracker-setting.png)|

還有另一種形式是做在壓舌帽上 FreeTrack上有許多同好分享的成果

Reference:

  * <a href="http://www.free-track.net/english/">FreeTrack</a>
