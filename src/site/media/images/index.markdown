---
layout: section
title: "图片"
description: "一图胜千言，说的是图像是每个页面中不可或缺的一部分。图片同时占据着页面下载字节数的绝大部分。在响应式设计中，按照设备特性变化的不仅有布局还有图片。"
introduction: "一图胜千言，说的是图像是每个页面中不可或缺的一部分。图片同时占据着页面下载字节数的绝大部分。在响应式设计中，按照设备特性变化的不仅有布局还有图片。"
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
  twitterauthor: "@petele"
article:
  written_on: 2014-04-30
  updated_on: 2014-08-02
  order: 1
collection: introduction-to-media
id: images
key-takeaways:
  use-right-image:
    - Use the best image for the characteristics of the display, consider
      screen size, device resolution and page layout.
    - Change the <code>background-image</code> property in CSS for high DPI
      displays using media queries with <code>min-resolution</code> and
      <code>-webkit-min-device-pixel-ratio</code>.
    - Use srcset to provide high resolution images in addition to the 1x
      image in markup.
    - Consider the performance costs when using JavaScript image replacement
      techniques or when serving highly compressed high resolution images to
      lower resolution devices.
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

<div class="media media--video">
  <iframe src="https://www.youtube.com/embed/vpRsLPI400U?controls=2&modestbranding=1&showinfo=0&utm-source=crdev-wf" frameborder="0" allowfullscreen=""></iframe>
</div>

### 响应式图片

响应式 Web 设计意味着根据设备特性变化的不仅有布局，还有图片。例如，在高分辨率设备上，就需要使用高分辨率的图片以保证图像的清晰度。一个只有50%宽度的图片可以在浏览器只有800px宽度的时候表现良好，但是却会在较狭窄的手机屏幕中占据太多的资源。图像变小了，而使用的带宽却并没有减小。

### 艺术指导

<img class="center" src="img/art-direction.png" alt="Art direction example"
srcset="img/art-direction.png 1x, img/art-direction-2x.png 2x">

图片有时需要做更加精细的处理：更改方向，进行裁剪，或者直接整张替换。这种情况下对图片所做的更改通常被称为艺术指导（Art Direction）。请查看 [responsiveimages.org/demos/](http://responsiveimages.org/demos/) 上更多的例子。

{% include modules/nextarticle.liquid %}

{% endwrap %}
