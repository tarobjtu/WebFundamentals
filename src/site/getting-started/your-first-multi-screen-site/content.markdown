---
layout: article
title: "创建网站内容和结构"
description: "内容是所有网站的最重要部分。在这篇课程中，我们将向你展示如何快速规划并构建你的首个跨终端网站。"
introduction: "内容是任何网站最重要的部分。所以设计要服务于内容，而不是设计支配内容。这个教程中，首先确定我们需要的内容，然后根据内容来创建结构，接着以简单的线性布局展示网页。线性布局在宽窄视口（ViewPort）方面具有良好效果。（注：ViewPort，视口、视觉窗口，即显示区域）"
notes:
  styling:
    - 样式一会来噢~
article:
  written_on: 2014-04-17
  updated_on: 2014-04-23
  order: 1
id: multi-screen-content
collection: multi-screen
rel:
  gplusauthor: https://plus.google.com/+PaulKinlan
  twitterauthor: "@Paul_Kinlan"
related-guides:
  create-amazing-forms:
    -
      title: 创建漂亮的表单
      href: input/form/
      section:
        id: user-input
        title: "Forms"
        href: input/form/
    -
      title: 正确地输入标签和名称
      href: input/form/label-and-name-inputs.html
      section:
        id: user-input
        title: "Forms"
        href: input/form/
    -
      title: 选择最佳的input类型
      href: input/form/choose-the-best-input-type.html
      section:
        id: user-input
        title: Forms
        href: input/form/
  video:
    -
      title: 有效使用视频
      href: media/video/
      section:
        id: introduction-to-media
        title: "Video"
        href: media/
    -
      title: 改变开始播放位置
      href: media/video/
      section:
        id: introduction-to-media
        title: "Video"
        href: media/
    -
      title: 包含一张视频的海报
      href: media/video/
      section:
        id: introduction-to-media
        title: "Video"
        href: media/
  images:
    -
      title: 有效使用图片
      href: media/images/
      section:
        id: introduction-to-media
        title: "Images"
        href: media/
    -
      title:  在页面构建中正确使用图片
      href: media/images/#images-in-markup
      section:
        id: introduction-to-media
        title: "Images"
        href: media/
    -
      title: 图片优化
      href: performance/optimizing-content-efficiency/image-optimization.html
      section:
        id: introduction-to-media
        title: "Images"
        href: media/

key-takeaways:
  content-critical:
    - 首先确定我们需要的内容。
    - 勾画出信息架构（IA）的窄、宽视口。
    - 创建页面的骨架图，含内容不含样式。
---

{% wrap content %}

{% include modules/toc.liquid %}

## 创建网页结构

确认我们的需求：

1.  一块描述我们高级产品 — “CS256：移动Web开发”教程–的区域
2.  一个表单，用于收集对我们产品感兴趣用户的信息
3.  一段深入描述和视频
4.  一些实际课程产品中的图片
5.  一个数据表格，用来支持产品理念的信息

{% include modules/takeaway.liquid list=page.key-takeaways.content-critical %}

我们还分别从窄视口和宽视口出发，列出了粗略的信息架构和布局。

<div class="demo clear" style="background-color: white;">
  <img class="g-wide--1 g-medium--half" src="images/narrowviewport.png" alt="Narrow Viewport IA">
  <img  class="g-wide--2 g-wide--last g-medium--half g--last" src="images/wideviewport.png" alt="Wide Viewport IA">
</div>

这很容易转化成用于指导项目后续工作的网页框架的粗略部分。

{% include_code _code/addstructure.html structure %}

## 向网页添加内容

该网站的基本部分已经完成。我们清楚这部分及其要展示的内容，并且知道这部分在整个信息架构中的各自位置。现在，我们开始扩建网站。

{% include modules/remember.liquid title="Note" inline="true" list=page.notes.styling %}

### 创建标题和表单

标题和注册申请表单是该页面的关键部分，必须立刻呈现给用户。

在标题模块中添加简单的文字来描述课程：

{% include_code _code/addheadline.html headline %}

我们还需要填充表单。表单简易，用于搜集用户的名字、电话、回他们电话的恰当时间。

所有的表单应该具有标签和placeholders（预期值的提示信息），以便于用户聚焦相应的元素，了解往其中应该填写的内容，还有利于协助工具理解表单结构。名称属性不仅用于把表单值传输到服务器，还用于浏览器针对用户如何自动填写表单问题上给出重要提示。

我们还添加了语义类型，使得用户能够更快、更简单地在移动设备上输入内容。例如，当输入电话号码时，拨号键盘应恰好呈现在用户眼前。

{% include_code _code/addform.html form %}

{% include modules/related_guides.liquid inline=true list=page.related-guides.create-amazing-forms %}

### 创建视频和信息区域

内容的视频、信息区域稍微复杂一些，包括了一个我们产品功能的项目符号列表，还包含一个展示我们产品服务于用户的预留视频。

{% include_code _code/addcontent.html section1 %}

视频通常以互动性较强的方式来描述内容，经常用来阐述一个产品或概念。

遵循最佳实践原则，你可以轻松地在你的网站整合视频：

*  添加`controls`属性，方便人们播放视频。
*  添加`poster`图片，提供内容预览。
*  添加多个`<source>`元素，以支持多种视频格式。
*  当窗口无法播放视频时，添加带视频链接的文本，供人们下载视频。

{% include_code _code/addvideo.html video html %}

{% include modules/related_guides.liquid inline=true list=page.related-guides.video %}

### 创建图片区域

没有图片的网站会略显枯燥。有两种类型的图片：

*  内容图片 &mdash; 嵌入文档的图片，用于传达其他内容信息。
*  样式图片 &mdash; 让网站看起来更漂亮的图片，包括背景图片、图案、渐变。我们将在[下篇文章]({{site.baseurl}}{{page.article.next.url}})中讲述。

图片区域是内容图片的集合。这些图片出现在我们的产品中。

Content images are critical to conveying the meaning of the page. Think of
them like the images used in newspaper articles.  The images we are using are
pictures of the tutors on the project:  Chris Wilson, Peter Lubbers and Sean
Bennet.

{% include_code _code/addimages.html images html %}

图片设置成与屏幕宽度一样宽。这个设置在移动设备上行之有效，但在桌面程序中表现平平。我们将在响应式设计部分讲述这个问题。

{% include modules/related_guides.liquid inline=true list=page.related-guides.images %}

Many people don't have the ability to view images and often use an assistive
technology such as a screen reader that will parse the data on the page and
relay that to the user verbally.  You should ensure that all your content
images  have a descriptive `alt` tag that the screen reader can speak out to
the user.

When adding `alt` tags make sure that you keep the alt text as concise as
possible to fully describe  the image.  For example in our demo we simply
format the attribute to be "Name: Role", this presents enough information
to the user to understand that this section is about the authors and what
their job is.

### 添加表格式数据部分

最后一部分是简单的表格，用于列出产品的详细统计数据。

表格仅限用于表格式数据，如信息矩阵。

{% include_code _code/addcontent.html section3 %}

### 添加页脚

大部分网站需要一个页脚，用来展示诸如条款和条件、免责声明等内容，以及无须出现在页面的主导航或主内容区域的其他内容。

在我们的网站中，我们将链接到使用条款和条件、联系页面、以及我们的社交帐号。

{% include_code _code/addcontent.html footer %}

## 总结

我们已经创建好了网站的大纲，确定了全部的主要框架元素。我们确信所有相关内容已经准备妥当，以满足我们业务的需求。

<div class="clear">
  <img class="g-wide--2 g-medium--half" src="images/content.png" alt="Content" style="max-width: 100%;">
  <img  class="g-wide--2 g-wide--last g-medium--half g--last" src="images/narrowsite.png" alt="" style="max-width: 100%;">
</div>

你会发现，网页现在看起来相当完美了，这是已经设计完的效果。内容是任何网站最重要的方面。我们需要确保拥有良好的信息架构和坚实的信息密度。这篇指南提供了优秀的创建网站基础。我们将在下一篇指南中为内容设计样式。

{% include modules/nextarticle.liquid %}

{% endwrap %}
