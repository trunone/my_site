---
layout: post
title: 移除資料夾以外之檔案執行權限
author: Chih-En Wu
tags:
- Linux
lang: zh_TW
---
{% highlight bash %}
$ find . -type f -print 0 | xargs -0 chmod a-x
{% endhighlight %}

* find . : 在目前路徑下尋找。

* -type f : 只尋找檔案 (-type d 則為尋找目錄)

* -print0 : 印出檔案名稱時，將各檔案名稱以 null 字元隔開。這可以避免檔名中有空白時判斷錯誤。

* xargs : 對每一個輸出的檔案執行一個命令。

* -0 : 以 null 字元為分隔來執行命令

* chmod a-x : 移除所有執行權限
