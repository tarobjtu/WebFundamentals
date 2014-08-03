---
layout: article
title: "快速通话"
description: "用户在有通话功能的设备上简单点击一个电话号码就能直接打电话给你。"
introduction: "用户在有通话功能的设备上简单点击一个电话号码就能直接打电话给你。"
article:
  written_on: 2014-06-17
  updated_on: 2014-08-02
  order: 1
id: click-to-call
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
  twitterauthor: "@petele"
collection: click-to-call
key-takeaways:
  c2c:     
    -  使用 <code>tel:</code> 语法链接电话号码
    -  总是使用国际化的电话格式
---

{% wrap content %}
<style type="text/css">
  img.center {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }
</style>

{% include modules/toc.liquid %}

{% include modules/takeaway.liquid list=page.key-takeaways.c2c %}

## 链接电话号码以快速通话

虽然很多现代浏览器会自动检测电话号码并将其转化为链接，但更好的方式是在你的代码里手动链接电话号码。
通过手动的给每个号码添加标记，你就能确保他们总是可以点击并且样式符合你网站的设计。

使用 `tel:` 语法将链接电话号码，语法如下：

{% highlight html %}
NIST Telephone Time-of-Day Service <a href="tel:+1-303-499-7111">+1 (303) 499-7111</a>
{% endhighlight %}

效果为:

NIST Telephone Time-of-Day Service <a href="tel:+1-303-499-7111">+1 (303) 499-7111</a>

<img src="images/click-to-call_framed.jpg" class="center" alt="Click to call example.">

在大多数有通话功能的设备中，用户需要在拨出号码前确认，以确保他们不会不小心拨出昂贵的长途号码。
如果设备不支持通话功能，浏览器将会显示一个菜单询问用户如何处理这串数字。

不支持声音呼叫的桌面浏览器会打开计算机上默认的电话应用，比如 Google Voice 或 Microsoft
Communicator。

## 使用国际化的电话格式

总是提供使用国际化格式的电话号码：
加号（+）、国家代号、地区代号和数字。
为了方便阅读和实现更好的自动化检测功能，最好用连字符（-）来分割这些代码和数字。

用连字符（-）连接的电话格式确保了来自世界各地的用户都能进行通话。

## 必要时禁用自动检测功能

现代的手机浏览器会自动检测电话号码以实现点击呼叫。
手机上的 Safari 浏览器会自动将电话号码转化为链接，并配上超链接样式。
手机上安卓版的 Chrome 浏览器也会自动将电话号码转化为链接，但并不会配上超链接样式。

在页面顶部添加以下这个 meta 标签来阻止手机端的 Safari 浏览器自动检测电话号码：

{% highlight html %}
<meta name="format-detection" content="telephone=no">
{% endhighlight %}

## 其他快速通话特色

除了 `tel:` 语法，一些现代浏览器也支持 `sms:` 和 `mms:` 但支持的并不一致，还有一些特色比如自动填写信息内容的功能也不一定支持。

{% endwrap %}
