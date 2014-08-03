---
layout: article
title: "Click to call"
description: "在具有电话功能的设备上，方便用户通过轻轻点击一串电话号码来直接联系你，这通常被称作 Click to call。"
introduction: "在具有电话功能的设备上，方便用户通过轻轻点击一串电话号码来直接联系你，这通常被称作 Click to call。"
article:
  written_on: 2014-06-17
  updated_on: 2014-06-17
  order: 1
id: click-to-call
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
  twitterauthor: "@petele"
collection: click-to-call
key-takeaways:
  c2c: 
    -  Wrap all phone numbers in hyperlinks with the <code>tel:</code> schema
    -  Always use the international dialing format
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

## 为电话号码创建 click to call 的链接

虽然许多现代移动浏览器会自动检测的电话号码并将其转换为链接，但直接在你的代码里做到这一点是个好主意。通过手动标记每个电话号码，就可以确保始终启用 click to call 的电话号码，而且他们将被样式化来搭配你的网站。

用 `tel:` 格式来标记一串电话号码为一个链接。语法很简单：

{% highlight html %}
NIST Telephone Time-of-Day Service <a href="tel:+1-303-499-7111">+1 (303) 499-7111</a>
{% endhighlight %}

结果是：

NIST Telephone Time-of-Day Service <a href="tel:+1-303-499-7111">+1 (303) 499-7111</a>

<img src="images/click-to-call_framed.jpg" class="center" alt="Click to call example.">

在大多数具有电话功能的设备上, 号码被拨之前用户将会收到一条确认，以保证用户不是正在被欺骗拨打价格昂贵的长途或者溢价的电话号码。当设备不支持电话呼叫功能时，用户可能会看到一个菜单来让他们选择如何让浏览器处理这些号码。

对于不支持语音呼叫的桌面浏览器会打开在计算机上默认的电话服务应用程序，比如 Google Voice 或者 Microsoft Communicator。

## 使用国际拨号格式

始终使用国际拨号格式来提供电话号码：加号（+），国家代码，地区代码和号码。虽然不是绝对必要的，但使用连字符（-）来分开每个数字段来方便您阅读和更好的自动检测是个好主意。

使用连字符连接的国际拨号格式，可确保用户的呼叫可以被接通，无论是从哪里呼叫，无论几百米甚至上千公里远。

## 在必要时禁用自动检测

现代移动浏览器会自动检测电话号码，并启用 click to call。移动端 Safari 会自动将电话号码转化为关联超链接样式的链接。安卓端 Chrome 浏览器会自动检测到电话号码并允许用户 click to call，但不会把号码包裹在超链接中，也不会对号码使用特殊的样式。

为了阻止移动端 Safari 自动检测电话号码，在页面代码顶部添加以下 meta 标签：

{% highlight html %}
<meta name="format-detection" content="telephone=no">
{% endhighlight %}

## click to call 的其他特点

除了 `tel:` 格式, 一些现代浏览器也支持 `sms:` 和 `mms:` 格式，尽管这些支持并不一致，而且像设置 message body 等一些功能也不总是奏效的。

{% endwrap %}
