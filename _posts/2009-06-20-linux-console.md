---
layout: post
title: Linux Console 解析度調整
date: '2009-06-20T20:04:00.000+08:00'
author: Chih-En Wu
tags:
- Linux
- Ubuntu
modified_time: '2011-07-28T13:10:34.841+08:00'
blogger_id: tag:blogger.com,1999:blog-6518933078301809282.post-496227588056563508
blogger_orig_url: http://trunone.blogspot.com/2009/06/linux-console.html
---

現在的螢幕解析度都很高了<br/><br/>但Linux預設的Console解析度都只有640x480<br/><br/>
能顯示的行數很少 為了能充份利用螢幕 就來吧解析度調高吧<br/><br/>
用文字編輯器打開以下的檔案：<br/><br/>
{% highlight text %}
/boot/grub/menu.lst
{% endhighlight %}
這是GRUB的設定檔 在裡面找到kernel開頭的一行<br/><br/>
{% highlight text %}
kernel /boot/vmlinuz-your-version ~~~~
{% endhighlight %}
在那一行的最後加上<br/><br/>
{% highlight text %}
kernel /boot/vmlinuz-your-version ~~~~ vga=???
{% endhighlight %}
???要填的數字請參考下列的表格，之後重開機就可以了

| Colors  || 640x400 || 640x480 || 800x600 || 1024x768 || 1152x864 || 1280x1024 || 1600x1200 |
|--------:||:-------:||:-------:||:-------:||:--------:||:--------:||:---------:||:---------:|
| 4 bits  ||   ?     ||  ?      || 770     ||  ?       || ?        || ?         || ?         |
| 8 bits  ||  768    || 769     || 771     ||  773     || 353      || 775       || 796       |
| 15 bits ||   ?     || 784     || 787     ||  790     || 354      || 793       || 797       |
| 16 bits ||   ?     || 758     || 788     ||  791     || 355      || 794       || 798       |
| 24 bits ||   ?     || 786     || 789     ||  792     || ?        || 795       || 799       |
| 32 bits ||   ?     ||  ?      || ?       ||  ?       || 356      || ?         || ?         |
