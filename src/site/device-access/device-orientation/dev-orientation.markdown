---
layout: article
title: "方向传感器"
description: "Device orientation返回设备旋转移动的数据，包括设备翻转，摇晃；检测设备所处的角度，方位，朝向（指南针）等。"
introduction: "Device orientation返回设备旋转移动的数据，包括设备翻转，摇晃；检测设备所处的角度，方位，朝向（指南针）等。"
article:
  written_on: 2014-06-17
  updated_on: 2014-06-17
  order: 1
id: device-orientation
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
  twitterauthor: "@petele"
collection: device-orientation
key-takeaways:
  长话短说: 
    -  慎用
    -  必要的兼容性检测
    -  界面更新不用和Device orientation事件的触发频率保持同步， 用异步<a href="https://developer.mozilla.org/zh-CN/docs/Web/API/window.requestAnimationFrame">requestAnimationFrame</a>取而代之
---

{% wrap content %}

{% include modules/toc.liquid %}

{% include modules/takeaway.liquid list=page.key-takeaways.devorientation %}

## Device orientation 应用场景

应用场景举例:

<ul>
  <li>用户移动时更新地图地图。</li>
  <li>界面微调，例如添加视差效果。</li>
  <li>结合地理定位信息，可用于逐向导航。</li>
</ul>

## 必要的兼容性检测

监听 `DeviceOrientationEvent`, 首页检测当前浏览器是否支持该事件，其次在`window` 对象上绑定 `deviceorientation`。

{% include_code _code/dev-orientation.html devori javascript %}

## Device orientation事件处理方式
当设备移动或者改变方向的时候，Device orientation事件将被触发，它返回设备在当前位置和之前位置的坐标差异数据，这些数据都是相对于<a href="index.html#earth-coordinate-frame">地球坐标系</a>。

Device orientation事件主要返回三个属性,
<a href="index.html#rotation-data">`alpha`</a>, 
<a href="index.html#rotation-data">`beta`</a>, and 
<a href="index.html#rotation-data">`gamma`</a>.  On Mobile Safari, and
在Safari移动浏览器上，还会额外返回 <a href="https://developer.apple.com/library/safari/documentation/SafariDOMAdditions/Reference/DeviceOrientationEventClassRef/DeviceOrientationEvent/DeviceOrientationEvent.html">`webkitCompassHeading`</a> 属性，它用于表明罗盘朝向。

{% endwrap %}
