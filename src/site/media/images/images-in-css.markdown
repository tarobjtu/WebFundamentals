---
layout: article
title: "CSS中的图像"
description: "CSS 的 `background` 属性是向元素添加复杂图像的有利工具，使多张图片添加、重复等操作更加便捷。与媒体查询结合时，background 属性变得更加强大，能按照屏幕分辨率，视口大小等有条件地加载图片。"
introduction: "CSS 的 `background` 属性是向元素添加复杂图像的有利工具，使多张图片添加、重复等操作更加便捷。与媒体查询结合时，background 属性变得更加强大，能按照屏幕分辨率，视口大小等有条件地加载图片。"
translator: '<a href="http://blog.jobbole.com/author/aimujie/" target="_blank">埃姆杰</a>、<a href="http://crimx.com" target="_blank">黄杰华(StrayBugs)</a>'
reviewer: '<a href="http://crimx.com" target="_blank">黄杰华(StrayBugs)</a>'
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
  twitterauthor: "@petele"
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 2
collection: images
key-takeaways:
  use-right-image:
    - 根据显示设备的特点选用最佳的图片，可以考虑屏幕大小，设备分辨率和页面布局。
    - 在 CSS 中利用媒体查询 <code>min-resolution</code> 和
      <code>-webkit-min-device-pixel-ratio</code> 改变 <code>background-image</code> 属性以获得高 DPI 显示。
    - 在提供原始 1x 大小图像的基础上使用 srcset 属性提供高分辨率图像。
    - 在使用 JavaScript 图像更换技术或者为低分辨率设备高压缩高分辨率图像时要考虑性能耗损。
  avoid-images:
    - Avoid images whenever possible, instead, leverage browser capabilities,
      use unicode characters in place of images, and replace complex icons
      with icon fonts.
  optimize-images:
    - Don't just randomly choose an image format, understand the different
      formats available, and use the format best suited.
    - Include image optimization and compression tools into your workflow to
      reduce file sizes.
    - Reduce the number of http requests by placing frequently used images
      into image sprites.
    - Consider loading images only after they’ve scrolled into view to
      improve the initial page load time and reduce the initial page weight.
remember:
  compressive:
    - Use caution with the compressive technique because of the increased
      memory and decoding costs it requires.  Resizing large images to fit on
      smaller screens is expensive and can be particularly painful on low-end
      devices where both memory and processing is limited.
related:
  optimize:
    - <a href="../../performance/optimizing-content-efficiency/optimize-encoding-and-transfer.html#image-optimization">Image optimization</a>
    - <a href="../../performance/optimizing-content-efficiency/">Optimizing content efficiency</a>
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

{% include modules/takeaway.liquid list=page.key-takeaways.use-right-image %}

## 为条件图片加载或艺术指导使用媒体查询

媒体查询不仅影响页面布局，还可以根据可视区域宽度有条件地加载图片或提供艺术指导。

下面的例子中， 在小屏幕设备上只会下载 `small.png` 并应用到 `div` 的内容中，而在大屏幕设备上则会将 `background-image: url(body.png)` 应用到 `body` 上，同时 `background-image: url(large.png)` 应用到 `div` 上。

{% include_code _code/conditional-mq.html conditional css %}

## 使用 image-set 提供高分辨率图片

CSS中的 `image-set()` 函数增强了 `background` 属性的表现，使得为不同的设备特性提供不同图片变得更容易。这允许浏览器根据设备特性选择最佳图像，例如在 2x 大小的显示屏上显示 2x 大小的图像，或者当 2x 设备网络带宽受限时显示 1x 图片。

{% highlight css %}
background-image: image-set(
  url(icon1x.jpg) 1x,
  url(icon2x.jpg) 2x
);
{% endhighlight %}

除了加载正确的图片外，浏览器还会将图片调整到合适的大小。换句话说，浏览器会假设 2x 图片的大小是 1x 图片的 2 倍，于是便会以 2 倍的比例缩小 2x 图片，所以页面上的图片看上去大小是一致的。

对 `image-set()` 函数的支持还很新，并且仅仅在带有 `-webkit` 厂商前缀的 Chrome 和 Safari 浏览器中支持。另外还要考虑在 `image-set()` 不起作用时引用备用图片，例如：

{% include_code _code/image-set.html imageset css %}

上面的样式会在支持 `image-set` 的浏览器中加载合适的资源，其它情况则使用 1x 大小的资源。明显需要注意的是浏览器对 `image-set()` 的支持度还很低，大多数浏览器会得到 1x 大小的资源。

## 使用媒体查询提供高分辨率图片或艺术指导

媒体查询能根据[设备像素比](http://www.html5rocks.com/en/mobile/high-dpi/#toc-bg)创建规则，为 2x 与 1x 大小屏幕指定不同的图片。

{% highlight css %}
@media (min-resolution: 2dppx),
(-webkit-min-device-pixel-ratio: 2)
{
  /* 这里提供高 dpi 的样式和资源 */
}
{% endhighlight %}

Chrome、Firefox 和 Opera 浏览器都支持 `(min-resolution: 2dppx)` 标准，而 Safari 和 Android 浏览器都需要旧式的厂商前缀写法，不带 `dppx` 单元。请记住，这些样式只会在设备匹配媒体查询时才加载，所以必须为基准情况指定样式。且这么做还能保证在浏览器不支持特定分辨率媒体查询的情况下渲染其它内容。

{% include_code _code/media-query-dppx.html mqdppx css %}

你也可以使用 min-width 语法根据视口大小显示可替代的图片。这项技术的好处在于与媒体查询不匹配的图像不会下载。比如 `bg.png` 只在浏览器宽度大于或等于 500px 时才会下载并应用到 `body` 上：

{% highlight css %}
@media (min-width: 500px) {
  body {
    background-image: url(bg.png);
  }
}
{% endhighlight %}

{% include modules/nextarticle.liquid %}

{% endwrap %}
