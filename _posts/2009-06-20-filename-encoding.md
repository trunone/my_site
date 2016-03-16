---
layout: post
title: 檔名編碼
date: '2009-06-20T20:41:00.002+08:00'
author: Chih-En Wu
tags:
- Windows
modified_time: '2011-07-28T14:17:52.326+08:00'
blogger_id: tag:blogger.com,1999:blog-6518933078301809282.post-991222160204984255
blogger_orig_url: http://trunone.blogspot.com/2009/06/blog-post.html
---

有時候在網路上下載檔案，檔名會變成 %xx%xx%xx 的亂碼

用記事本把這段存成 code.js

{% highlight javascript %}
var fso;
fso = new ActiveXObject("Scripting.FileSystemObject");
for(i=0; i<WScript.Arguments.length; i++){
    fso.MoveFile( WScript.Arguments(i), decodeURI(WScript.Arguments(i)) );
}
{% endhighlight %}

再把問題檔案拉到 code.js 上，就會轉成正確檔名了。
