---
layout: article
title: "运动传感系统"
translator: <a href="http://lison.sinaapp.com" target="_blank">李昕</a>
reviewer: （待校正）
description: "设备运动传感系统能够设定的场景下将设备的运动状态返回给我们，包括设备运动加速度和转速。"
introduction: "设备运动传感系统能够设定的场景下将设备的运动状态返回给我们，包括设备运动加速度和转速。"
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
  devmotion:
    -  在需要获取当前时刻运动信息时调用设备运动传感系统。
    -  <code>rotationRate</code> 提供的设备转速是以 &deg;/sec 为单位。
    -  <code>acceleration</code> 和 <code>accelerationWithGravity</code> 提供的设备运动加速度是以 m/sec<sup>2</sup> 为单位。
    -  了解不同浏览器在设备运动传感系统相关实现上的区别。
---

{% wrap content %}

{% include modules/toc.liquid %}

{% include modules/takeaway.liquid list=page.key-takeaways.devmotion %}

## 何时调用设备运动传感系统提供的事件

其实身边有很多场景需要使用设备运动传感系统提供的事件，举几个栗子：

<ul>
  <li>通过晃动设备触发数据更新。</li>
  <li>游戏中，我们常常会需要通过设备的运动实现对人物运动的控制。</li>
  <li>健康和健身类的应用中对设备运动传感系统的需求就不言而喻了。</li>
</ul>

## 检查浏览器兼容性并监听对应事件

实现设备运动事件监听：首先，先检查设备浏览器是否支持设备运动事件，假如存在，则在全局变量`window`上添加事件监听器；

{% include_code _code/jump-test.html devmot javascript %}

## 如何处理事件所提供的数据

设备运动事件会在有规律的时间间隔上被触发并返回设备的转速（单位：&deg;/s）和运动加速度（单位：m/s<sup>2</sup>）。需要注意，部分设备由于硬件受限无法返回除去重力加速外的加速度。

设备运动事件被触发的同时会返回四个属性值，
<a href="index.html#device-frame-coordinate">`accelerationIncludingGravity`</a>,
<a href="index.html#device-frame-coordinate">`acceleration`</a>,
（除去重力加速外的加速度），
<a href="index.html#rotation-data">`rotationRate`</a> 和 `interval`.

举个栗子，将手机水平向上地放置在水平桌面上。

<table class="table-4">
  <colgroup>
    <col span="1">
    <col span="1">
    <col span="1">
    <col span="1">
  </colgroup>
  <thead>
    <tr>
      <th data-th="State">运动状态</th>
      <th data-th="Rotation">转速</th>
      <th data-th="Acceleration (m/s<sup>2</sup>)">加速度（不含重力加速度）(m/s<sup>2</sup>)</th>
      <th data-th="Acceleration with gravity (m/s<sup>2</sup>)">加速度（含重力加速度）(m/s<sup>2</sup>)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="State">静止</td>
      <td data-th="Rotation">[0, 0, 0]</td>
      <td data-th="Acceleration">[0, 0, 0]</td>
      <td data-th="Acceleration with gravity">[0, 0, 9.8]</td>
    </tr>
    <tr>
      <td data-th="State">垂直向上运动</td>
      <td data-th="Rotation">[0, 0, 0]</td>
      <td data-th="Acceleration">[0, 0, 5]</td>
      <td data-th="Acceleration with gravity">[0, 0, 14.81]</td>
    </tr>
    <tr>
      <td data-th="State">仅向右水平运动</td>
      <td data-th="Rotation">[0, 0, 0]</td>
      <td data-th="Acceleration">[3, 0, 0]</td>
      <td data-th="Acceleration with gravity">[3, 0, 9.81]</td>
    </tr>
    <tr>
      <td data-th="State">同时垂直向上并向右运动</td>
      <td data-th="Rotation">[0, 0, 0]</td>
      <td data-th="Acceleration">[5, 0, 5]</td>
      <td data-th="Acceleration with gravity">[5, 0, 14.81]</td>
    </tr>
  </tbody>
</table>

相反地，如果手机是被握着的，通常屏幕会垂直于地面并正对着用户：

<table class="table-4">
  <colgroup>
    <col span="1">
    <col span="1">
    <col span="1">
    <col span="1">
  </colgroup>
  <thead>
    <tr>
      <th data-th="State">运动状态</th>
      <th data-th="Rotation">转速</th>
      <th data-th="Acceleration (m/s<sup>2</sup>)">加速度（不含重力加速度）(m/s<sup>2</sup>)</th>
      <th data-th="Acceleration with gravity (m/s<sup>2</sup>)">加速度（含重力加速度）(m/s<sup>2</sup>)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="State">静止</td>
      <td data-th="Rotation">[0, 0, 0]</td>
      <td data-th="Acceleration">[0, 0, 0]</td>
      <td data-th="Acceleration with gravity">[0, 9.81, 0]</td>
    </tr>
    <tr>
      <td data-th="State">垂直向上运动</td>
      <td data-th="Rotation">[0, 0, 0]</td>
      <td data-th="Acceleration">[0, 5, 0]</td>
      <td data-th="Acceleration with gravity">[0, 14.81, 0]</td>
    </tr>
    <tr>
      <td data-th="State">仅向右水平运动</td>
      <td data-th="Rotation">[0, 0, 0]</td>
      <td data-th="Acceleration">[3, 0, 0]</td>
      <td data-th="Acceleration with gravity">[3, 9.81, 0]</td>
    </tr>
    <tr>
      <td data-th="State">同时垂直向上并向右运动</td>
      <td data-th="Rotation">[0, 0, 0]</td>
      <td data-th="Acceleration">[5, 5, 0]</td>
      <td data-th="Acceleration with gravity">[5, 14.81, 0]</td>
    </tr>
  </tbody>
</table>

### 案例：利用设备运动传感系统提供的接口计算设备最快的加速度

常见的设备运动传感系统使用场景是计算设备最快的加速度。举个栗子，我们需要通过计算设备最快的加速度来估算人在跳跃过程中最快的加速度。

{% include_code _code/jump-test.html devmothand javascript %}

在点击“GO!”按钮后，网页会开始统计设备的加速度，并提示你进行跳跃；在完成跳跃后，网页会统计出跳跃过程中的最大加速度。

{% endwrap %}
