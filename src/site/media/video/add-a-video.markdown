---
layout: article
title: "添加视频文件"
description: " 学习使用最简单的方法为你的网站添加视频，确保用户在任何设备上都能得到最佳的体验。"
introduction: "学习使用最简单的方法为你的网站添加视频，确保用户在任何设备上都能得到最佳的体验。"
article:
  written_on: 2014-04-16
  updated_on: 2014-07-31
  order: 1
collection: videos
key-takeaways:
  add-a-video:
    - 在网站上用视频元素来加载、解码并播放视频。
    - 制作视频的多种格式来覆盖广泛的移动平台。
    - 视频的大小正确，保证它们不会溢出。
    - 可访问性也很重要，添加轨道元素作为视频元素的子元素。
remember:
  media-fragments:
    - Media Fragments API 支持大多数平台，但是不支持IOS平台。
    - 确保你的服务器支持Range Requests（范围请求）。Range Requests在默认情况下被大多数服务器所启用，但一些托管服务可能会将其关闭。
---

{% wrap content%}

{% include modules/toc.liquid %}

<style>

  img, video, object {
    max-width: 100%;
  }

  img.center {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }

</style>

{% include modules/takeaway.liquid list=page.key-takeaways.add-a-video %}

## 添加视频元素

在网站上用 `<video>` 视频元素加载、解码并播放视频:

<video controls>
     <source src="video/chrome.webm" type="video/webm">
     <source src="video/chrome.mp4" type="video/mp4">
     <p>浏览器不支持视频元素</p>
</video>

{% highlight html %}
<video src="chrome.webm" type="video/webm">
    <p>浏览器不支持视频元素</p>
</video>
{% endhighlight %}

## 指定多个文件格式

不是所有浏览器都支持相同的视频格式的，`<source>` 元素可以让你指定多种格式作为备选，以防用户的浏览器不支持某些格式。举例来说：

{% include_code _code/video-main.html sourcetypes %}

当浏览器解析 `<source>` 标签时，它将使用可选的 `type` 属性来帮助决定下载哪个文件或是播放哪个文件。如果浏览器支持 WebM 格式的话，它会播放 chrome.webm 文件，如果不支持，它会检查其是否能支持 MPEG-4 视频的播放。
可以参考
<a href='//www.xiph.org/video/vid1.shtml' title='Highly entertaining and informative video guide to digital video'>《极客们的数字媒体入门》</a>
来找到更多有关网络上的音频和视频是如何工作的。

这种方法比起HTML上不同的服务或是服务器端脚本来讲有诸多优势，尤其是在移动端：

* 开发人员可以按照优先顺序列出格式
* 原生客户端切换减少了等待时间;只发出一个请求来获取内容
* 让浏览器来选择一种格式更简单、更快，也能也比用用户代理检测来使服务器支持数据库更可靠。
* 制定每个文件源的类型提高了网络性能；该浏览器可以直接选择一个视频源，而无需对先下载一部分视频来识别视频的格式。

这几点对于移动设备尤为重要，这里带宽和延时都很紧张，用户忍耐度也非常有限。而当多个源带有不支持格式时，没有引入 `type` 属性也会影响到性能。

使用你的手机浏览器开发者工具，比较一下{% link_sample _code/video-main.html %}有 type 属性{% endlink_sample %}和{% link_sample _code/notype.html %}没有用到 type 属性{% endlink_sample %}时的网络活动情况。同时检查一下你浏览器开发者工具的响应标题，[确保你的服务器报告了正确的 MINE 类型](//developer.mozilla.org/en/docs/Properly_Configuring_Server_MIME_Types)；否则视频源的类型检查将无法正常工作。

## 指定开始和结束时间

节省带宽，并使你的网站反映更灵敏：使用Media Fragments API接口来为视频元素添加开始时间和结束时间。

<video controls>
  <source src="video/chrome.webm#t=5,10" type="video/webm">
  <source src="video/chrome.mp4#t=5,10" type="video/mp4">
  <p>浏览器不支持视频元素</p>
</video>

添加一个媒体片段（media fragment），你只需要简单的将 `#t=[开始时间][,结束时间]` 代码加入到媒体的URL中，举个例子，如果想播放视频的第五秒到第十秒这段内容，只需要：

{% highlight html %}
<source src="video/chrome.webm#t=5,10" type="video/webm">
{% endhighlight %}

你还可以用Media Fragments API来提供对于一个视频的多个图像——就像DVD中的提示点一样 &ndash; 而不用编码或是提供于多个文件。

{% include modules/remember.liquid title="记住" list=page.remember.media-fragments %}

用你的浏览器开发者工具，在响应标题中检查 `Accept-Ranges: bytes` :

<img class="center" alt="Chrome Dev Tools screenshot: Accept-Ranges: bytes" src="images/Accept-Ranges-Chrome-Dev-Tools.png">

## 包含海报图片

在视频元素中添加一个 `poster` 属性，从而你的用户将在这些元素加载时就对视频内容有所了解，而不需要在下载视频或是开始播放之后才知道其内容。

{% highlight html %}
<video poster="poster.jpg" ...>
  ...
</video>
{% endhighlight %}

如果视频的src受损或者所提供的视频格式全部不被支持时，poster也可以是一个备选。poster图像的唯一缺点是会有一个额外的文件请求，这回消耗一定的带宽并且需要渲染。如果想了解更多信息，请参见[图像优化](../../performance/optimizing-content-efficiency/optimize-encoding-and-transfer.html#image-optimization)。

下面是两个并列在一起比较的无海报图片和含有海报图片的视频 &ndash; 我们将海报图像做成灰度图来证明其不是视频。

<div class="clear">
  <div class="g--half">
    <img class="center" alt="Android Chrome screenshot, portrait: no poster" src="images/Chrome-Android-video-no-poster.png">
  </div>

  <div class="g--half g--last">
    <img class="center" alt="Android Chrome screenshot, portrait: with poster" src="images/Chrome-Android-video-poster.png">
  </div>
</div>

{% include modules/nextarticle.liquid %}

{% endwrap %}
