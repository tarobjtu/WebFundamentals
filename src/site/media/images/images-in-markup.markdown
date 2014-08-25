---
layout: article
title: "带标签的图片"
description: "<code>img</code> 元素十分强大 – 它能够下载，解析并渲染内容 – 且现代浏览器支持多种图像格式。引入能够跨设备的图像，与放置专为桌面浏览器定制的图像没什么不同，只需要几个小调整就能有很好的体验。"
introduction: "<code>img</code> 元素十分强大 – 它能够下载，解析并渲染内容 – 且现代浏览器支持多种图像格式。引入能够跨设备的图像，与放置专为桌面浏览器定制的图像没什么不同，只需要几个小调整就能有很好的体验。"
translator: '<a href="http://blog.jobbole.com/author/aimujie/" target="_blank">埃姆杰</a>、<a href="http://crimx.com" target="_blank">黄杰华(StrayBugs)</a>'
reviewer: '<a href="http://crimx.com" target="_blank">黄杰华(StrayBugs)</a>'
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
  twitterauthor: "@petele"
article:
  written_on: 2014-04-30
  updated_on: 2014-08-04
  order: 1
collection: images
key-takeaways:
  img-in-markup:
    - 图片使用相对大小以避免意外溢出容器。
    - 当需要根据设备特征（亦称艺术指导，art direction）来指定不同图片时，使用 <code>picture</code> 元素。
    - 在 <code>img</code> 元素中使用 <code>srcset</code> 和 <code>x</code> 描述符来提示浏览器在不同密度下选择最佳图片。
remember:
  picture-support:
    - <code>picture</code> 元素还在<b>开发中</b>，在2014年6月之前只有日更版（nightly）可用。因为其强向后兼容性和 
      <a href="http://picturefill.responsiveimages.org/">Picturefill</a> 插件的支持，我们现在就引入进来但建议您谨慎使用。详情参看
       <a href="http://responsiveimages.org/#implementation">
      ResponsiveImages.org</a>。 
  compressive:
    - 谨慎使用压缩技术，因为它需要占用更多内存并且需要解码。调整图像以适合小屏幕的代价是非常昂贵的，在内存和处理能力都非常有限的低端设备上更会是苦不堪言。
---

{% wrap content%}

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

{% include modules/toc.liquid %}

{% include modules/takeaway.liquid list=page.key-takeaways.img-in-markup %}


## 图片使用相对大小

在指定图片宽度时，请记得使用相对单位以防止图片意外溢出视口。例如 `width: 50%;` 会使图片宽度变成容器元素（不是视口或实际像素）宽度的50%。

因为 CSS 允许内容溢出它的容器，有必要使用 `max-width: 100%` 防止图片及其他元素溢出。例如：

{% highlight css %}
img, embed, object, video {
  max-width: 100%;
}
{% endhighlight %}

确保使用 `alt` 属性为 `img` 元素提供有意义的描述，这些措施能提高网站的可访问性，更好地为屏幕阅读器等辅助设备提供上下文。

## 使用 `img` 标签的 `srcset` 属性为高DPI设备优化

`srcset` 属性强化了 `img` 元素的行为，使其更容易为不同设备提供不同图片文件。与 CSS 中的 `image-set` [CSS function](images-in-css.html#use-image-set-to-provide-high-res-images) 相似，`srcset` 允许浏览根据设备特性选择最佳图片，例如在 2x 大小的显示屏上显示 2x 的图片，或者当 2x 设备在网络带宽受限时显示 1x 大小的图片。

{% highlight html %}
<img src="photo.png" srcset="photo@2x.png 2x" ...>
{% endhighlight %}

在那些不支持 `srcset` 的浏览器上，浏览器只会简单地显示 `src` 属性指定的默认图像。这就是为什么一定要包含 1x 大小的图片，因为它能在所有的设备上显示。支持  `srcset` 属性的浏览器会解析由英文逗号分割的 图像/条件 列表，只有最合适的图像才会被下载和显示。

虽然条件项有很多内容包括像素密度、宽度和高度等等，但目前只有像素密度被广泛支持。要平衡当前的表现与未来的特性，总是在属性中指定 2x 大小的图片就可以了。

## `picture` - 响应式图片的艺术指导

根据设备特性改变图片，即艺术指导（Art Direction）可以由 `picture` 元素来完成。为了实现根据不同设备特点提供图片的不同版本，`picture` 元素定义了一套声明式的解决方案。比如设备大小，设备分辨率，方向，等等。

<img class="center" src="img/art-direction.png" alt="Art direction example"
srcset="img/art-direction.png 1x, img/art-direction-2x.png 2x">

{% include modules/remember.liquid title="Important" list=page.remember.picture-support %}

当图片要在多种设备中显示或者响应式设计要求在不同屏幕大小中显示不同图片时，就要考虑用 `picture` 元素。与 `video` 元素一样，这里可以包含多个 `source`，就可以根据媒体查询（media query）或图片格式来指定不同图片。

{% include_code _code/media.html picture html %}

上面的例子中，如果浏览器宽度在 800px 以上，那么 `head.jpg` 与 `head-2x.jpg` 之一会被使用，取决于设备的分辨率。如果浏览器是在 450px 到 800px 之间，那么`head-small.jpg` 与 `head-small-2x.jpg` 之一会被使用，也是取决于设备的分辨率。当为了向后兼容或不支持 `picture` 时，浏览器会渲染 `img` 元素，所以记得加上去。

### 图片相对大小

当图片最终大小不可知时，很难去为图片源指定密度描述符。尤其是当图片宽度需要根据浏览器大小按比例动态变化。

不用提供固定的大小和密度，在图片元素大小后面加上一个宽度描述符 `w`，让浏览器自动计算有效像素密度，选择最佳的图片下载。

{% include_code _code/sizes.html picture html %}

上面的例子渲染了一张占视口一半宽度的图片（`sizes="50vw"`），然后根据浏览器的宽度与设备像素比，不管浏览器窗口有多大，浏览器都能选择正确的图片。下面的表格说明了浏览器如何选择图片：

<table class="table-4">
  <colgroup>
    <col span="1">
    <col span="1">
    <col span="1">
    <col span="1">
  </colgroup>
  <thead>
    <tr>
      <th data-th="Browser width">浏览器宽度</th>
      <th data-th="Device pixel ratio">设备像素比</th>
      <th data-th="Image used">图片选择</th>
      <th data-th="Effective resolution">有效分辨率</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Browser width">400px</td>
      <td data-th="Device pixel ratio">1</td>
      <td data-th="Image used"><code>200.png</code></td>
      <td data-th="Effective resolution">1x</td>
    </tr>
    <tr>
      <td data-th="Browser width">400px</td>
      <td data-th="Device pixel ratio">2</td>
      <td data-th="Image used"><code>400.png</code></td>
      <td data-th="Effective resolution">2x</td>
    </tr>
    <tr>
      <td data-th="Browser width">320px</td>
      <td data-th="Device pixel ratio">2</td>
      <td data-th="Image used"><code>400.png</code></td>
      <td data-th="Effective resolution">2.5x</td>
    </tr>
    <tr>
      <td data-th="Browser width">600px</td>
      <td data-th="Device pixel ratio">2</td>
      <td data-th="Image used"><code>800.png</code></td>
      <td data-th="Effective resolution">2.67x</td>
    </tr>
    <tr>
      <td data-th="Browser width">640px</td>
      <td data-th="Device pixel ratio">3</td>
      <td data-th="Image used"><code>1000.png</code></td>
      <td data-th="Effective resolution">3.125x</td>
    </tr>
    <tr>
      <td data-th="Browser width">1100px</td>
      <td data-th="Device pixel ratio">1</td>
      <td data-th="Image used"><code>1400.png</code></td>
      <td data-th="Effective resolution">1.27x</td>
    </tr>
  </tbody>
</table>


### 为响应式图片声明断点

很多情况下，图片的大小需要依据网站的布局断点改变。比如在小屏幕上，图片可能要占满视口的宽度，而在大屏幕上，它可能只占一小部分。

{% include_code _code/breakpoints.html picture html %}

上面例子的 `size` 属性使用了几个媒体查询来指定图片的大小。当浏览器宽度大于 600px 时，图片会占视口宽度的 25%；当宽度为 500px 到 600px 之间时，图片会占视口宽度的 50%；低于 500px 则占满整个视口宽度。

## 其他图像技术

### 压缩图片

[图像压缩技术](http://www.html5rocks.com/en/mobile/high-dpi/#toc-tech-overview)为所有设备提供高压缩的 2x 大小图片，而不论设备的实际性能。根据图像的类型和压缩级别，图像质量看上去可能没有太大的变化，但其大小会显著降低。

{% link_sample _code/compressive.html %}
参见例子
{% endlink_sample %}

{% include modules/remember.liquid title="Important" list=page.remember.compressive %}

### JavaScript 图像替代方案

JavaScript 图像替代是指先检查设备的性能参数，然后“见机行事”。可以通过 `window.devicePixelRatio` 来检测设备像素比，`width` 和 `height` 取得宽高，甚至可以通过 `navigator.connection` 去嗅探网络连接或者发送一个假请求。得到这些信息之后你就可以决定什么情况下加载什么图片。

这种方法最大的一个缺点是使用 JavaScript 意味着图片会延迟加载至少到前瞻解析器（look-ahead parser）完成后。也就是说图片在 `pageload` 事件发射前都不会开始下载。此外，浏览器将最有可能下载 1x 和 2x 大小的图像，从而增加了页面权重。

{% include modules/nextarticle.liquid %}

{% endwrap %}
