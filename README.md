Web Fundamentals翻译工作
=======================
Web Fundamentals是非常好的跨终端WEB学习教程，翻译这系列教程的初衷是作为团队新入职的童鞋和实习生的新人Landing教程。幸运的是[伯乐在线](http://blog.jobbole.com/)一群志同道合的小伙伴也在翻译Web Fundamentals，而且已经有三十多篇文章的产出。与伯乐在线翻译负责人@黄利民沟通后，我决定共同合作，完成这个振奋人心的工作，希望更多小伙伴阅读Web Fundamentals并从中受益。

Web Fundamentals还会有很多英文原文陆续出炉，我们的翻译需要更多有志之士参与其中，有意者请Q我（490483792，备注：翻译Web Fundamentals）。

翻译好的文章会定期更新到[study.f2e.me](http://study.f2e.me/)与[伯乐在线](http://blog.jobbole.com/)供大家浏览。

翻译问题汇总
-----------
好的产品是不断倾听用户需求、磨合迭代出来的，好的译文同样需要你的批评和吐槽。有任何翻译质量问题，请留言到issues


Web Fundamentals
================

Web Fundamentals定位为多终端Web开发技术文档中心。志在为当今web开发者建造一个像iOS Dev Center或developer.android.com一样全面且有用的教程。


内容规划
------------

通过Github的Issues和[站点结构与内容清单](http://goo.gl/nWDD0M)来查看Web Fundamentals的内容规划。


版本状态
--------------

2014年四月底项目顺利开启，同年六月正式发布第一版，现在已经进入每六周为周期的迭代中。

技术
----------

这是一个Jekyll创建的网站。

```
/src
  /appengine - the server to host the static content
  /site - the documentation
    /getting-started - the getting started articles
    /multi-device-layouts - responsive design guide
    /introduction-to-media - the guide to using media
    /optimizing-performance - the perf articles
    /using-touch - managing touch
    /showcase - the case-studies
```

Jekyll生成的`/build` 文件夹中的内容不会被提交到git仓库中。

安装依赖
=======

Mac
---

1. 安装 [XCode Command Line Tools](https://developer.apple.com/xcode/downloads/)
1. 安装 [RVM](https://rvm.io/rubies/default)
    * `curl -sSL https://get.rvm.io | bash`
1. 设置RVM的默认模式为：2.0.0
    * `rvm install ruby-2.0.0-p451`
    * `rvm --default use 2.0.0`
1. 安装 [Pygments](http://pygments.org/)
    * `easy_install pygments`
1. 安装 [RubyGems](https://rubygems.org/) 依赖 ([Jekyll](http://jekyllrb.com/), [Kramdown](http://kramdown.gettalong.org/) and [Sass](http://sass-lang.com/install)) 
    * cd src/ && `bundle install`
1. 安装 [Node.js](http://nodejs.org/)
1. 安装 [Grunt CLI](http://gruntjs.com/)
    * `npm install -g grunt-cli`


Using project-level meta data
=============================

The table of contents is generated from `src/site/_project.yaml`

To parse the `_project.yaml` file, include `{% injectdata content _project.yaml %}` in the page. You then have access to the variables in the page object.


Generating Table of Contents
----------------------------

The table of contents is generated from `src/site/_book.yaml`

To parse the `_book.yaml` file, include `{% injectdata content _book.yaml %}` in the page and then iterate as follows:

     {% for section in page.content.toc %}
        SOME MARKUP
     {% endfor %}

Jekyll Special elements
-----------------------

* Code import: `{% highlight javascript %} {% include sample1.js %} {% endhighlight %}`
* `{{ articles _category_}}` a list of articles in divs, ordered by the "order" preamble.
* `{{ showcases _category_}}` a list of showcases.
