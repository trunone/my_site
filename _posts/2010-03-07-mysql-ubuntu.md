---
layout: post
title: 改變MySQL資料庫的位置 (Ubuntu)
date: '2010-03-07T15:11:00.005+08:00'
author: Chih-En Wu
tags:
- Linux
- Ubuntu
- MySQL
modified_time: '2011-08-01T16:31:42.842+08:00'
blogger_id: tag:blogger.com,1999:blog-6518933078301809282.post-1182086087653779518
blogger_orig_url: http://trunone.blogspot.com/2010/03/mysql-ubuntu.html
---

<h1><span style="color: #ff0000;">!!!做以下動作前最好備份一下資料庫!!!</span></h1>

首先把 MySQL 停下來

{% highlight bash %}$ sudo /etc/init.d/mysql stop{% endhighlight %}

接下來複製資料庫到你想要的位置

{% highlight bash %}$ sudo cp -R -p /var/lib/mysql /path/to/new/datadir{% endhighlight %}

再來編輯MySQL的設定檔，這裡我是使用 vim，可用自己習慣的

{% highlight bash %}$ sudo vim /etc/mysql/my.cnf{% endhighlight %}

找到 *datadir* 這個變數，把後面的路徑改成新的

接下來這一步如果不是 Ubuntu 7.10 以上可以不用做 (不過大部分都是了吧？)

Ubuntu 7.10 以上用了一個叫 AppAromr 的程式來保護系統檔

必需改變它的設定，不然是無法從新的路徑讀到 MySQL 資料庫的

所以來編輯它MySQL設定的部分
{% highlight bash %}$ sudo gedit /etc/apparmor.d/usr.sbin.mysqld{% endhighlight %}
有兩行是原始路徑 */var/lib/mysql* 可以直接改成新的路徑

如果不放心，可以在前面加#號，然後複製成新的兩行去改

接下來就重新啟動 AppArmor 與 MySQL
{% highlight bash %}$ sudo /etc/init.d/apparmor reload
$ sudo /etc/init.d/mysql restart
{% endhighlight %}
如果啟動的過程中沒有出現錯誤訊息的話，那就大功告成了！

Reference: <a href="">How to change the MySQL data default directory</a>
