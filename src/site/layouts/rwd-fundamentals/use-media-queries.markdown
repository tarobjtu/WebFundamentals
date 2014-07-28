---
layout: article
title: "用CSS媒体查询实现响应式"
description: "Much of the web isn't optimized for those multi-device experiences. Learn the
             fundamentals to get your site working on mobile, desktop or anything else with a screen."
introduction: "媒体查询（Media queries）是一种可以应用在CSS样式上的简易过滤器，它可以根据设备的渲染特性（包括显示类型、宽度、高度、转向甚至是分辨率）来显示不同的样式。"
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 3
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
  twitterauthor: "@petele"
collection: rwd-fundamentals
key-takeaways:
  set-viewport:
    - Use meta viewport tag to control the width and scaling of the browsers viewport.
    - Include <code>width=device-width</code> to match the screen's width in device independent pixels.
    - Include <code>initial-scale=1</code> to establish a 1:1 relationship between CSS pixels and device independent pixels.
    - Ensure your page is accessible by not disabling user scaling.
  size-content-to-vp:
    - Do not use large fixed width elements.
    - Content should not rely on a particular viewport width to render well.
    - Use CSS media queries to apply different styling for small and large screens.
  media-queries:
    - 媒体查询可以根据设备特性应用不同的样式。
    - 使用<code>min-width</code>确保最大的体验程度。
    - 对元素使用相对大小，防止布局被破坏。
  choose-breakpoints:
    - Create breakpoints based on content, never on specific devices, products or brands.
    - Design for the smallest mobile device first, then progressively enhance the experience as more screen real estate becomes available.
    - Keep lines of text to a maximum of around 70 or 80 characters.
remember:
  use-commas:
    - Use a comma to separate attributes to ensure older browsers can properly parse the attributes.
---
{% wrap content %}

<style>
  .smaller-img {
    width: 60%;
    display: block;
    margin-left: auto;
    margin-right: auto;
  }

  img.center {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }

  video.responsiveVideo {
    width: 100%;
  }
</style>


{% include modules/toc.liquid %}

{% include modules/takeaway.liquid list=page.key-takeaways.media-queries %}


举个例子，你可以把所有需要应用的打印上的样式放入打印媒体查询中：

{% highlight html %}
<link rel="stylesheet" href="print.css" media="print">
{% endhighlight %}

除了在样式表的链接上使用`media`属性，还有另外两种方式可以实现媒体查询：在CSS文件中添加`@media`和`@import`。出于性能的考虑，前两个方法都比使用`@import`要好。

{% highlight css %}
@media print {
  /* print style sheets go here */
}

@import url(print.css) print;
{% endhighlight %}

媒体查询使用的逻辑不是互斥的，如果过滤器发现符合了某一标准，那么利用CSS的优先级规则使得对应的样式可以生效。

## 根据视口大小使用媒体查询

媒体查询使得响应式的体验得以实现：根据屏幕尺寸的不同，特定的样式得以应用。有了媒体查询语句，就可以根据设备的不同特性应用不同的样式了。

{% highlight css %}
@media (query) {
  /* CSS Rules used when query matches */
}
{% endhighlight %}

虽然有很多设备属性都可以作为查询依赖的条件，不过最经常使用的还是`min-width`、`max-width`、 `min-height`和`max-height`。


<table class="table-2">
  <colgroup>
    <col span="1">
    <col span="1">
  </colgroup>
  <thead>
    <tr>
      <th data-th="attribute">属性</th>
      <th data-th="Result">结果</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="attribute"><code>min-width</code></td>
      <td data-th="Result">浏览器宽度超过某个值的时候，定义在查询中的样式就会生效。</td>
    </tr>
    <tr>
      <td data-th="attribute"><code>max-width</code></td>
      <td data-th="Result">浏览器宽度小于等于某个值的时候，定义在查询中的样式会生效。</td>
    </tr>
    <tr>
      <td data-th="attribute"><code>min-height</code></td>
      <td data-th="Result">浏览器高度超过某个值的时候，定义在查询中的样式会生效。</td>
    </tr>
    <tr>
      <td data-th="attribute"><code>max-height</code></td>
      <td data-th="Result">浏览器高度小于等于某个值的时候，定义在查询中的样式会生效。</td>
    </tr>
    <tr>
      <td data-th="attribute"><code>orientation=portrait</code></td>
      <td data-th="Result">当浏览器高度大于等于宽度的时候，样式将会生效。</td>
    </tr>
    <tr>
      <td data-th="attribute"><code>orientation=landscape</code></td>
      <td data-th="Result">当浏览器宽度大于等于高度的时候，样式将会生效。</td>
    </tr>
  </tbody>
</table>

来看看下面这个例子：

<figure>
  {% link_sample _code/media-queries.html %}
    <img src="imgs/mq.png" class="center" srcset="imgs/mq.png 1x, imgs/mq-2x.png 2x" alt="Preview of a page using media queries to change properties as it is resized.">
  {% endlink_sample %}
</figure>

{% include_code _code/media-queries.html mqueries %}

* 当浏览器宽度在<b>0px</b>到<b>640px</b>之间，`max-640px.css`就会生效。
* 当浏览器宽度在<b>500px</b>到<b>600px</b>之间，在`@media`中定义的样式会生效。
* 如果浏览器是在<b>640px</b>或者以上的，`min-640px.css`会生效。
* 如果浏览器的<b>宽度大于高度</b>，`landscape.css`就会生效。
* 如果浏览器的<b>高度大于宽度</b>，portrait.css就会生效。


## `min-device-width`的说明

还可以根据 `*-device-width`来设置查询条件，但是**非常不鼓励**使用这种方式。 

The difference is subtle but very important: `min-width` is based on the 
size of the browser window, whereas `min-device-width` is based on
the size of the screen.  Unfortunately some browsers, including the legacy 
Android browser may not report the device width properly and instead 
report the screen size in device pixels instead of the expected viewport width. 

In addition, using `*-device-width` can prevent content from adapting on 
desktops or other devices that allow windows to be resized because the query
is based on the actual device size, not the size of the browser window.

## Use relative units

A key concept behind responsive design is fluidity and proportionality as
opposed to fixed width layouts.  Using relative units for measurements can help
simplify layouts and prevent accidentally creating components that are too big
for the viewport.

For example, setting width: 100% on a top level div, ensures that it spans the
width of the viewport and is never too big or too small for the viewport.  The
div will fit, no matter if it's a 320px wide iPhone, 342px wide Blackberry Z10
or a 360px wide Nexus 5.

In addition, using relative units allows browsers to render the content based on
the users zoom level without the need for adding horizontal scroll bars to the
page.

<div class="clear">
  <div class="g--half">
    <h2 class="text-danger text-center">NO</h2>
{% highlight css %}div.fullWidth {
  width: 320px;
  margin-left: auto;
  margin-right: auto;
}{% endhighlight %}
  </div>

  <div class="g--half g--last">
    <h2 class="text-success text-center">YES</h2>
{% highlight css %}div.fullWidth {
  width: 100%;
}{% endhighlight %}
  </div>
</div>

{% include modules/nextarticle.liquid %}

{% endwrap %}
