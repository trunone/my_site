---
layout: post
title: Plurk RSS Bot
date: '2010-03-07T10:46:00.003+08:00'
author: Chih-En Wu
tags:
- Plurk
- PHP
modified_time: '2012-03-26T11:22:34.167+08:00'
blogger_id: tag:blogger.com,1999:blog-6518933078301809282.post-2497433540876114266
blogger_orig_url: http://trunone.blogspot.com/2010/03/plurk-rss-bot.html
---

這個Bot可能要有架站的人來用比較方便 因為是用<a href="http://www.php-cli.com/">PHP CLI</a>
我是用在Ubuntu上 不過Windows應該也沒有問題的 只是要再自己查一下資料

首先因會用到一個PHP的module叫cURL 通常預設是不會裝的 所以要來安裝一下
{% highlight bash %}# sudo apt-get install curl php5-curl{% endhighlight %}
接下來要去抓別人寫來抓RSS的PHP Code 我是用<a href="http://simplepie.org/">SimplePie</a>

抓完以後解開它的壓縮檔 裡面有一個simplepie.inc把它拿出來

再來把以下的原始碼存成PlurkBot.php 也放在和simplepie.inc同一個路徑
{% highlight php %}
<?php
define('NICKNAME', '你的帳號');
define('PASSWORD', '你的密碼');
define('USER_ID', '你的user_id'); //這裡比較麻煩 要到你的plurk去看原始碼 user_id那個變數就是了
// Include SimplePie
// Located in the parent directory
include_once('simplepie.inc');
//
// Create a new instance of the SimplePie object
$feed = new SimplePie();
//
// Use the URL that was passed to the page in SimplePie
$feed->set_feed_url('http://chinese.engadget.com/rss.xml'); //這段網址可以改成你要的RSS 這邊我是用Engadget Chinese來示範
//
// Initialize the whole SimplePie object.  Read the feed, process it, parse it, cache it, and
// all that other good stuff.  The feed's information will not be available to SimplePie before
// this is called.
$success = $feed->init();
//
// We'll make sure that the right content type and character encoding gets set automatically.
// This function will grab the proper character encoding, as well as set the content type to text/html.
$feed->handle_content_type();
//
$pu_number = 1;
//
foreach($feed->get_items() as $item) {
$plurk_pu[$pu_number] = 'News: '.$item->get_permalink().' ('.ereg_replace(' \(([0-9]{1,2}) 回應)$','' , $item->get_title()).')';
//這一段我有對取得的RSS標題做修改 因為Engadget的RSS標題最後會有幾人回應的字 我覺得會怪怪的 所以把它處理掉
$pu_number++;
}
//
$show = mt_rand(1, 5); //這行是從取得的RSS標題中的前五個隨機選一個
//
$ch = curl_init();
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_COOKIEJAR, 'plurk.cookie');
curl_setopt($ch, CURLOPT_COOKIEFILE, 'plurk.cookie');
//
// login
curl_setopt($ch, CURLOPT_URL, '');
curl_setopt($ch, CURLOPT_POSTFIELDS, 'nick_name='.NICKNAME.'&password='.PASSWORD);
curl_exec($ch);
//
// post
curl_setopt($ch, CURLOPT_URL, '');
curl_setopt($ch, CURLOPT_POSTFIELDS, 'qualifier=%3A&content='.urlencode($plurk_pu[$show]).'&no_comments=0&uid='.USER_ID);
curl_exec($ch);
//
curl_close($ch);
?>
{% endhighlight %}
記得把內容改為符合你自己的Plurk

然後在同一個路徑新增一個資料夾cache 權限改為777 這是給SimplePie放cache用的

再來就是最後一步 執行：
{% highlight bash %}# php PlurkBot.php{% endhighlight %}你就會發現你的Plurk上自動噗了一則Engadget的新聞囉

那如果你還希望它定時執行的話 那用把它放到<a href="http://en.wikipedia.org/wiki/Cron">Crontab</a>去吧！

Reference: <a href="http://blog.xuite.net/vexed/tech/22023458">自製Plurk Bot定時自動發噗</a>
