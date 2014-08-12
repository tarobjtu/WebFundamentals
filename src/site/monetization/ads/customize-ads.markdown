---
layout: article
title: "个性化定制广告"
translator: <a href="http://lison.sinaapp.com" target="_blank">李昕</a>
reviewer: （待校正）
description: "好的广告往往能够改善用户体验。但广告内容来源于各式各样的厂商，而他们提供的内容也是各不相同；因此需要对广告的类型、颜色、大小以及位置有全面地把控。"
introduction: "好的广告往往能够改善用户体验。但广告内容来源于各式各样的厂商，而他们提供的内容也是各不相同；因此需要对广告的类型、颜色、大小以及位置有全面地把控。"
article:
  written_on: 2014-07-31
  updated_on: 2014-08-12
  order: 3
id: customize-ads
collection: ads
key-takeaways:
  tldr:
    - 绝对不要将广告放置在可能影响用户使用习惯的位置；确保广告在页面中所处的位置不会影响主体内容。
    - 尽量使用响应式的广告模块；如果智能大小变化仍无法满足需要，可以使用高级模式。
    - 充分利用广告位置，使其填满广告文字和图片，使得利益最大化。
    - 合理地在内容中穿插广告提高广告的曝光率。
    - 选择能够是网站整体形成良好混搭、衬托和对比的文字样式。
notes:
  targeting:
    - Ads are targeted based on overall site content, not keywords or categories. If you'd like to display ads related to specific topics, include complete sentences and paragraphs about these topics.
  testing:
    - 无论何时都要记得在各种设备和不同尺寸屏幕上测试广告模块，以确保响应式正常工作。
  images:
    - 广告提供商有权利决定广告长成什么样。你所能做的只是选择什么样类型的广告以及广告的位置和大小，但你无法控制广告的内容。
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

{% include modules/takeaway.liquid list=page.key-takeaways.tldr %}

## 将广告放置在最能让用户接受的位置

当我们在考虑如何放置广告以及放置广告的数量时，用户是我们首要考虑的因素！

* 广告只能是对原内容的扩充，绝对不可以是其他形式。
* 页面中存在影响主体内容展示、占据用户主要的视觉感知空间或是没有清楚明确的广告标签的广告都会影响用户使用网站的满意度同时这些方式也违背了AdSense的广告策略。
* 确保广告有利于用户。如某广告模块产生的利润少的可怜或是导致了页面访问量、点击量下降，我们就可以认为这些广告对于用户毫无价值。

下面是如何在移动设备上安排广告位置的案例：

<img src="images/mobile_ads_placement.png" class="center" alt="Sample mobile image ad">

如果想了解更多，欢迎访问AdSense[关于如何安排广告位置的最佳实践经验](https://support.google.com/adsense/answer/1282097)。


## 如何应对响应式布局中广告空间不够？
在某些场景下，在处理广告模块时需要考虑的不仅仅是将其实现响应式展示。此时，你可以考虑使用高级模式替代响应式广告。例如使用GoogleAdSense提供的[媒体检索]({{site.baseurl}}/layouts/rwd-fundamentals/use-media-queries.html)实现对广告内容大小的精确控制：

1. 按照说明开发常见的响应式广告单元。
2. 在Ad的代码生成器中，选择高级模式。
3. 根据实际使用场景中广告模块的尺寸填入准确的大小参数:

{% highlight html %}
<style type="text/css">
  .adslot_1 { width: 320px; height: 50px; }
  @media (min-width:500px) { .adslot_1 { width: 468px; height: 60px; } }
  @media (min-width:800px) { .adslot_1 { width: 728px; height: 90px; } }
</style>
<ins class="adsbygoogle adslot_1"
    style="display:block;"
    data-ad-client="ca-pub-1234"
    data-ad-slot="5678"></ins>
<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<script>(adsbygoogle = window.adsbygoogle || []).push({});</script>
{% endhighlight %}

{% link_sample _code/customize.html %}
  试一试
{% endlink_sample %}

查看[高级功能](https://support.google.com/adsense/answer/3543893)

{% include modules/remember.liquid title="Important" list=page.notes.testing %}

## 最大程度地挖掘广告位的议价潜力

网站的广告位越具有竞争力，广告商也更愿意花钱投放。如何最大程度地挖掘广告位的议价能力呢：

* 确保广告位同时能够承载文字或是图片。排除任意一种方式就等于限制了能够购买你的广告位的广告商。
* 尽量使用常见的尺寸来设计广告位，例如300px或是250px（参考[广告尺寸手册](https://support.google.com/adsense/answer/6002621)）。

## 选择能够兼容网页风格的样式

[好的广告](https://support.google.com/adsense/answer/17957)模块能够很好地衬托原来的站点风格。Google AdSense提供了[系列广告样式](https://support.google.com/adsense/answer/6002585)；选择最适合你的网站的部分进行整合。

### 什么叫可定制化

你可以对文字广告模块进行自定义，包括下面这些样式：

* Border color
* Background color
* 文字的 font family 和 font size
* 默认的文字 color
* 广告标题的文字 color
* 链接文字的 color

### 如何使用样式

当你在创建新的广告模块时，可以展开<strong>文字广告的样式</strong>属性进行配置：

<img src="images/customize.png" class="center" alt="Text ad styles">

所有文字使用的是Google AdSense的<strong>默认</strong>字体。当然你可以使用自定义的样式。

当你创建了一份自定义的样式，就可以将它应用于原有或是新建的广告模块：

1. 切换到[Ad Styles](https://www.google.com/adsense/app#myads-springboard/view=AD_STYLES)。
2. 从<strong>可选的样式列表</strong>中选择你需要的样式。
3. 对样式代码进行修改并<strong>保存</strong>。

当你修改了已存在的样式，任何关联了这份样式的广告模块的样式都会被更新。

{% include modules/remember.liquid title="Note" list=page.notes.images %}

{% endwrap %}
