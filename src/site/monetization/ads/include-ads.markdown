---
layout: article
title: "把广告引入你的网站"
description: "跟着这篇教程里的步骤，你将学到如何将广告放入到你的网站中。
这篇教程将按照以下这些步骤教会你如何在你的网站中放入广告。1. 创建AdSense账户。2. 创建广告单元。3. 将广告单元放到你的网站中。4. 配置你的支付设置。5. 盈利"
introduction: "跟着这篇教程里的步骤，你将学到如何将广告放入到你的网站中。
这篇教程将按照以下这些步骤教会你如何在你的网站中放入广告。1. 创建AdSense账户。2. 创建广告单元。3. 将广告单元放到你的网站中。4. 配置你的支付设置。5. 盈利"
article:
  written_on: 2014-07-31
  updated_on: 2014-07-31
  order: 2
id: include-ads
collection: ads
key-takeaways:
  tldr: 
    - To create an AdSense account, you must be 18, have a Google Account, and address.
    - Your website must be live before submitting an application, and the website content must comply with AdSense policies.
    - Create responsive ad units to ensure that your ads fit, no matter what device a user views them on.
    - Verify payment settings and wait for the money to start rolling in.
notes:
  crawler:
    - Make sure you're not blocking the AdSense crawler from accessing your site (see <a href="https://support.google.com/adsense/answer/10532">this help topic</a>). 
  body:
    - Paste all ad code within the body tag; otherwise the ads won't work.
  smarttag:
    - The <code>data-ad-client</code> and <code>data-ad-slot</code> will be unique for each ad you generate.
    - The <code>data-ad-format=auto</code> tag in the generated ad code enables the smart sizing behavior for the responsive ad unit.
---

{% wrap content %}

{% include modules/toc.liquid %}

{% include modules/takeaway.liquid list=page.key-takeaways.tldr %}

## 创建一个带有广告的示例页面

在这个引导中，你将使用Google AdSense 和Web Starter Kit 创建一个带有响应式广告的简单页面

<img src="images/ad-ss-600.png" sizes="100vw" 
  srcset="images/ad-ss-1200.png 1200w, 
          images/ad-ss-900.png 900w,
          images/ad-ss-600.png 600w, 
          images/ad-ss-300.png 300w" 
  alt="Sample website with ads on desktop and mobile">

如果你还不熟悉Web Start Kit， 请参考
[Set Up Web Starter Kit]({{site.baseurl}}/tools/setup/setup_kit.html) 这篇文档。

为了将广告引入到你的网站中并盈利吗，你需要完成以下这些步骤：

1. 创建一个AdSense 账号
2. 创建广告单元
3. 将广告单元放置到你的网站中
4. 配置你的支付设置

## 创建AdSense 账号
你需要一个激活的AdSense账号来为你网站上的广告提供支持。如果你现在还没有AdSense账号的话，你需要[创建一个账号](https://www.google.com/adsense/)并同意AdSense 的服务条款。创建账号的时候你需要确认以下这些内容：

* 你已满18岁并且拥有一个已验证的Google账号
* 你拥有一个符合[Google AdSense 程序政策](https://support.google.com/adsense/answer/48182)的仍在运行的网站或者其他的在线内容，广告将被存放在这个网站。
* 你有一个与你银行账号关联的邮寄地址和邮件地址，这样你才可以收到付款

## 创建广告单元

广告单元是呈现在你网站上的一系列广告，当你将我们提供的Javascript代码放到你的页面里时，这些广告就会出现。你有三种可选的方式来控制广告单元的大小：

* **[响应式(推荐的)](https://support.google.com/adsense/answer/3213689)**. 
* [预定义](https://support.google.com/adsense/answer/6002621).
* [自定义尺寸](https://support.google.com/adsense/answer/3289364).

你正在创建一个响应式的网站，所以使用响应式的广告单元。响应式广告会根据设备的尺寸和父元素的宽度自动地调整自己的大小。响应式广告在你响应式布局的“行”中工作，确保你的网站在任何设备上都看起来很棒

如果你不使用响应式的广告单元，你就需要写很多代码来控制广告在不同设备上显示的方式。即使你一定要明确规定广告单元的尺寸，你也可以使用响应式广告单元的[高级模式]({{site.baseurl}}/monetization/ads/customize-ads.html#what-if-responsive-sizing-isnt-enough)。

为了让你的代码更加简单也为了节省你的时间和工作，响应式广告单元的代码会自动将广告单元适配到你的页面布局中。代码会依据父容器的尺寸动态地计算合适的尺寸，然后选出在这个容器中表现最好的尺寸。举个例子，在一个360px宽度的移动优先的网站理，会显示一个320x50的广告单元

去[Google AdSense 的广告尺寸说明](https://support.google.com/adsense/answer/6002621#top)中看一下目前
[表现最佳的广告尺寸](https://support.google.com/adsense/answer/6002621#top)



### 为了创建响应式的广告单元你需要

1. 访问[My ads 标签](https://www.google.com/adsense/app#myads-springboard).
2. 点击 <strong>+New ad unit</strong>.
3. 给你的广告单元起一个名字，尽量把这个名字起的具有描述性，因为这个名字会出现在嵌入到页面中的代码里面
4. 在选择广告尺寸的下拉菜单中选择<strong>响应式</strong>。
5. 在广告类型下拉菜单中选择<strong>Text & display ads</strong>。
6. 点击 <strong>Save and get code</strong>保存并获取代码。
7. 在出现的<strong>广告代码</strong>盒子中，从模式下拉菜单中选择Smart sizing（推荐的）选项。这个模式是被推荐的模式，它不需要你在广告代码中做任何修改

创建好广告单元以后，AdSense 提供一个用来嵌入到站点中的代码片段，类似于于下面这种形式

{% highlight html %}
<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<!-- Top ad in web starter kit sample -->
<ins class="adsbygoogle"
  style="display:block"
  data-ad-client="XX-XXX-XXXXXXXXXXXXXXXX"
  data-ad-slot="XXXXXXXXXX"
  data-ad-format="auto"></ins>
<script>
  (adsbygoogle = window.adsbygoogle || []).push({});
</script>
{% endhighlight %}

{% include modules/remember.liquid title="小贴士" list=page.notes.smarttag %}

## 将广告单元引入到你的站点中

为了把广告引入到页面中，我们需要提供给我们的广告代码片段粘贴到我们的html标记中。如果你想引入多个广告，你也可以重复使用同一个广告单元，或者创建多个广告单元。

1. 打开`app`文件夹中的`index.html`。
2. 把提供的代码片段粘贴到`main`标签中。
3. Save the file and try viewing it in your browser, then try opening it on a 
mobile device or via the Chrome emulator.

{% include modules/remember.liquid title="Remember" list=page.notes.body %}

<div>
  <a href="/web/fundamentals/resources/samples/monetization/ads/">
    <img src="images/ad-ss-600.png" sizes="100vw" 
      srcset="images/ad-ss-1200.png 1200w, 
              images/ad-ss-900.png 900w,
              images/ad-ss-600.png 600w, 
              images/ad-ss-300.png 300w" 
      alt="Sample website with ads on desktop and mobile">
    <br>
    Try it
  </a>
</div>

## 配置支付的设置

在想什么时候你的AdSense付款会到吗？在尝试搞清楚你会在这个月还是下个月收到付款？确保你完成了下面的步骤：

1. 在[payee profile](https://www.google.com/adsense/app#payments3/h=BILLING_PROFILE)页面确认你已经提供了需要的税收信息
2. 确认你的收款人姓名还有地址是正确的
3. 在[支付设定页面](https://www.google.com/adsense/app#payments3/h=ACCOUNT_SETTINGS).选择你的收款形式
4. 输入你的[个人认证密码(PIN)](https://support.google.com/adsense/answer/157667).。这个PIN确认你账户信息的准确性
5. 检查你的余额是否达到了[支付的最低额](https://support.google.com/adsense/answer/1709871). 

如果你还有什么其他问题的话，请参考[AdSense付款介绍](https://support.google.com/adsense/answer/1709858)

{% endwrap %}
