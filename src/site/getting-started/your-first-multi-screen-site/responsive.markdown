---
layout: article
title: "让网站自适应"
description: "The web is accessible on a huge range of devices from small-screen phones to huge-screen televisions. Learn how to build a site that works well across all these devices."
introduction: "The web is accessible on a huge range of devices from small-screen phones through to huge-screen televisions. Each device presents its own unique benefits and also constraints. As a web developer, you are expected to support all ranges of devices."
key-takeaways:
  make-responsive:
    - 始终使用视口（viewport）。
    - 始终从窄视口开始，然后扩展。
    - 对内容进行响应适配时，设置临界点（breakpoints）开关。
    - 创建跨多临界点的高级视觉布局。
rel:
  gplusauthor: https://plus.google.com/+PaulKinlan
  twitterauthor: "@Paul_Kinlan"
related-guides:
  responsive:
    -
      title: 设置视口
      href: layouts/rwd-fundamentals/#set-the-viewport
      section:
        id: rwd-fundamentals
        title: "Responsive Web design"
        href: layouts/rwd-fundamentals/
    -
      title: 调整内容大小以适应视口
      href: layouts/rwd-fundamentals/#size-content-to-the-viewport
      section:
        id: rwd-fundamentals
        title: "Responsive Web design"
        href: layouts/rwd-fundamentals/
  first-break-point:
    -
      title: 使用“媒介查询”
      href: layouts/rwd-fundamentals/#use-css-media-queries-for-responsiveness
      section:
        id: rwd-fundamentals
        title: "Responsive Web design"
        href: layouts/rwd-fundamentals/
    -
      title: 布局模式
      href: layouts/rwd-patterns/
      section:
        id: rwd-patterns
        title: "Layout Pattens"
        href: layouts/rwd-patterns/
    -
      title: 主要的流式布局
      href: layouts/rwd-patterns/#mostly-fluid
      section:
        id: rwd-patterns
        title: "Responsive Web design"
        href: layouts/rwd-patterns/
  images:
    -
      title: "针对高保真dpi设备，使用srcset属性来增强图片效果"
      href: media/images/images-in-markup.html#enhance-imgs-with-srcset-for-high-dpi-devices
      section:
        id: images
        title: "Images"
        href: media/images/
    - 
      title: "使用媒介查询，以提供高分辨率的图片或艺术设计"
      href: media/images/images-in-css.html#use-media-queries-for-conditional-image-loading-or-art-direction
      section:
        id: images
        title: "Images"
        href: media/images/

notes:
  styling:
    - We have assumed a set of styles that include color, padding and font styling that match our brand guidelines.
  not-all-at-once:
    - 无须马上调整所有元素，必要时进行微调。
article:
  written_on: 2014-04-17
  updated_on: 2014-04-23
  order: 2
collection: multi-screen
id: multi-screen-responsive
---

{% wrap content %}

{% include modules/toc.liquid %}

我们着手建立一个网站，可以运行于多尺寸屏幕、不同类型设备上。在[前一篇文章]({{site.baseurl}}{{page.article.previous.url}})中，我们精心构建了网页的信息架构，创建了一个基本结构。在本指南中，我们将结合基本结构与内容，把它制作成一个漂亮的网页，可自适应不同的屏幕尺寸。

<div class="clear">
  <figure class="g-wide--2 g-medium--half">
    <img  src="images/content.png" alt="Content" style="max-width: 100%;">
    <figcaption>{% link_sample _code/content-without-styles.html %} 内容和结构 {% endlink_sample %} </figcaption>
  </figure>
  <figure class="g-wide--2 g-wide--last g-medium--half g--last">
    <img  src="images/narrowsite.png" alt="Designed site" style="max-width: 100%;">
    <figcaption>{% link_sample _code/content-with-styles.html %} 最终网站 {% endlink_sample %} </figcaption>
  </figure>
</div>

根据“移动优先”（Mobile First）的web开发原则，我们从窄视口开始 &mdash; 类似于手机 &mdash; 并首先形成经验。然后，我们扩展至更大的设备类。我们可以使视图变得更宽，判断设计、布局是否合适。

早些时候，我们创建几个不同的高层次设计，解决如何显示我们的内容。现在，我们需要让页面适应这些不同的布局。我们是这样做的：基于内容适应屏幕大小，决定临界点的位置 &mdash; 布局和样式发生改变的一个值点。

{% include modules/takeaway.liquid list=page.key-takeaways.make-responsive %}

## 添加一个视口

即使对于一个基本页面，你必须始终包含一个viewport 元数据标签。视口是建立多屏体验的最重要的组成部分。没有它，你的网站将无法良好运行于移动设备上。

视口用于提示浏览器：网页页面需要进行调整以适应屏幕范围。你可以为视口指定多种配置，以控制页面的显示。我们推荐一个默认值：

{% include_code _code/viewport.html viewport %}

视口元素位于文档头部，仅需声明一次。

{% include modules/related_guides.liquid inline=true list=page.related-guides.responsive %}

## 使用简单的样式

Our product and company already has a very specific branding and font guide-lines supplied
in a style guide.
我们产品和公司信息根据样式指南提供了一个非常具体的品牌、字体指导方针。

### 样式指南

样式指南是深入认识页面的可视化表达的有效途径。它有助于确保设计首尾风格一致。

#### 颜色

<div class="styles" style="font-family: monospace;">
  <div style="background-color: #39b1a4">#39b1a4</div>
  <div style="background-color: white">#ffffff</div>
  <div style="background-color: #f5f5f5">#f5f5f5</div>

  <div style="background-color: #e9e9e9">#e9e9e9</div>
  <div style="background-color: #dc4d38">#dc4d38</div>
</div>

### 添加样式化图片

在前篇指南中，我们添加了所谓的“内容图片”。这些图片对于描述我们产品很重要。样式图片不是核心内容的一部分，但增添了视觉冲击力，或引导用户注意力至特定内容。

这方面的一个很好的例子是：顶部内容的标题图片。它经常被用来吸引用户阅读更多的产品。

<div class="g-wide--2 g-wide--last g-medium--half g--last">
  <img  src="images/narrowsite.png" alt="Designed site" style="max-width: 100%;">
</div>

它们可以非常简单地包含进来。在我们的例子中，样式图片为背景，应用简单的css即可。

{% highlight css %}
#headline {
  padding: 0.8em;
  color: white;
  font-family: Roboto, sans-serif;
  background-image: url(backgroundimage.jpg);
  background-size: cover;
}
{% endhighlight %}

我们选择了一张模糊的简单背景图片，因此并不会影响网页内容。我们将它设置为`cover`，并总是以拉伸同时保持正确纵横比的方式来遍布整个元素。

<br style="clear: both;">

## 设置首个临界点

当宽度大约为600px时，设计开始变得糟糕。在我们的例子中，行的长度会超过10个字（最佳的阅读长度），而这正是我们需要调整的地方。

<video controls poster="images/firstbreakpoint.png" style="width: 100%;">
  <source src="videos/firstbreakpoint.mov" type="video/mov"></source>
  <source src="videos/firstbreakpoint.webm" type="video/webm"></source>
  <p>Sorry your browser doesn't support video.
     <a href="videos/firstbreakpoint.mov">Download the video</a>.
  </p>
</video>

6600px似乎是我们创建第一个临界点的良好位置，因为它确定了范围，重新定位元素，使之更好地适应屏幕。我们使用一种称为[媒介查询（Media Queries）]({{site.baseurl}}/layouts/rwd-fundamentals/#use-css-media-queries-for-responsiveness)的技术，可做到这一点。

{% highlight css %}
@media (min-width: 600px) {

}
{% endhighlight %}

更大的屏幕意味着拥有更多的空间，因此，在如何显示内容的问题上具有更强的灵活性。

{% include modules/remember.liquid title="Note" list=page.notes.not-all-at-once %}

从当前我们产品页面的效果看来，接下来我们需要：

*  约束设计的最大宽度
*  修改元素内边距和减少文本尺寸
*  移动表单，与标题内容浮动对齐
*  确保视频浮动于内容周围
*  减少图像尺寸，显示于更合适的网格

{% include modules/related_guides.liquid inline=true list=page.related-guides.first-break-point %}

## 限制设计界面的最大宽度

我们仅选择两大布局：窄视口和宽视口：这大大简化了构建过程。

我们决定，在窄视口中创建全幅部分，并且在宽视口中仍保持全幅。这意味着我们应限制屏幕的最大宽度，使得文本、段落不延伸成一长单行，出现超宽屏幕。我们选择800px作为最大值。

为了实现这个目标，我们需要限制宽度，并将元素置于中心。在每个主要区域中，我们需要创建一个容器，将其外边距（margin）设为auto。这允许屏幕增大，但内容仍处于中心，最大尺寸为800px。

如下所示，容器是一个简单的`div`：

{% highlight html %}<div class="container">...</div>{% endhighlight %}

{% include_code _code/fixingfirstbreakpoint.html containerhtml html %}

{% include_code _code/fixingfirstbreakpoint.html container css %}

## 改变内边距和减少文本尺寸

在窄视口中，我们没有大量空间来显示内容。因此，排版尺寸和磅值往往需大幅减少，以适应屏幕。

在更宽视口中，我们需要考虑用户倾向于更大的屏幕，甚至更大。为了增加内容的可读性，我们可以增加排版的尺寸和磅值，也可以改变内边距，以使不同区域更加明显。

在我们产品页面中，我们通过设置宽度方向的内边距为5%，以增加区域元素的内边距。我们也将增加每个部分顶部的大小。

{% include_code _code/fixingfirstbreakpoint.html padding css %}

## 调整元素以适应宽视口

窄视口以线性方式堆叠显示。每个主要区域及其里面的内容是依次从上到下排列。

宽视口提供了额外的空间，使得内容能以最佳方式呈现在屏幕上。对于我们的产品页面，根据信息架构，意味着我们可以：

*  移动表单，贴近头标题信息
*  将视频放在重要功能列表右边
*  平铺图像
*  展开表格

### 使表单元素浮动

窄视口意味着拥有较少的横向空间，不能充裕地放置屏幕上的元素。

为了更有效地利用屏幕的横向空间，我们需要打破顶部的线性流式布局，移动表单和表项，使得彼此紧邻。

{% include_code _code/fixingfirstbreakpoint.html formfloat css %}

{% include_code _code/fixingfirstbreakpoint.html padding css %}

<video controls poster="images/floatingform.png" style="width: 100%;">
  <source src="videos/floatingform.mov" type="video/mov"></source>
  <source src="videos/floatingform.webm" type="video/webm"></source>
  <p>Sorry your browser doesn't support video.
     <a href="videos/floatingform.mov">Download the video</a>.
  </p>
</video>

### 使视频元素浮动

在窄视口中，将视频设计为占屏幕的整个宽度，放置在重要功能列表后面。在宽视口中，当视屏位于功能列表后面时，视频变得太大，看起来不合适。

视频元素需移出窄视口的垂直流式布局，应与内容的项目符号列表并列显示。

{% include_code _code/fixingfirstbreakpoint.html floatvideo css %}

### 平铺图片

在窄视口（大部分移动设备）接口中，图像设置为屏幕的整个宽度、垂直堆叠。这在宽视口中得不到很好地扩展。

为了使图片在宽视口中看起来合适，将图片宽度缩放容器的30%，水平放置（而不是窄视口的垂直放置）。我们还将增加边框半径和盒子阴影（box-shadow），使图像看起来更吸引人。

<img src="images/imageswide.png" style="width:100%">

{% include_code _code/fixingfirstbreakpoint.html tileimages css %}

### 让图片自适应DPI

使用图片时，要考虑视口大小、显示分辨率。

在过去，网页专为96dpi屏幕而设计。随着移动设备的出现，我们已见证了屏幕像素密度的逐渐增大，更别说笔记本电脑的Retina显示屏了。因此，被编码为96dpi的图像，往往在高保真dpi设备上看起来很糟糕。

我们有一个还没被广泛采用的解决方案。对于支持该方案的浏览器，你可以在高分辨显示器上显示高像素的图像。

{% highlight html %}
<img src="photo.png" srcset="photo@2x.png 2x">
{% endhighlight %}

{% include modules/related_guides.liquid inline=true list=page.related-guides.images %}

### 表格

表格很难合适地展示在窄视口的设备上，需要特殊考虑。

在窄视口中，我们建议将表分成两排，把标题和表格单元调到一排，呈列状。

<video controls poster="images/responsivetable.png" style="width: 100%;">
  <source src="videos/responsivetable.mov" type="video/mov"></source>
  <source src="videos/responsivetable.webm" type="video/webm"></source>
  <p>Sorry your browser doesn't support video.
     <a href="videos/responsivetable.mov">Download the video</a>.
  </p>
</video>

在我们的网站中，必须单独为表格内容创建一个额外的临界点。由于最初是为移动设备构造网页，去掉已应用的样式是困难的，所以我们必须在宽视口css中关闭窄视口下表格的部分css。这向我们呈现了一个明确、连贯变化。

{% include_code _code/content-with-styles.html table-css css %}

## 结束语

**祝贺你**。当你阅读至此，你可创建你第一个产品的简单登陆页面，可跨大量不同设备、不同比例的表单、以及不同屏幕尺寸。

如果你遵循这些原则，你将有一个良好的开端：

1.  写代码之前，创建一个基本的信息架构和清楚需要的内容
2.  总是设置一个视口
3.  移动优先，形成基本的经验
4.  一旦拥有移动经验，增加显示器的宽度，直到网页看起来不合适，并在此设置临界点
5.  不断迭代

{% include modules/nextarticle.liquid %}

{% endwrap %}
