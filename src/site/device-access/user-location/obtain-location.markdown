---
layout: article
title: "获取用户当前位置"
introduction: "地理位置（Geolocation）API 能让你在用户允许情况下获取其位置信息。这个功能可以作为用户请求的一部分，
               比如导航用户到指定位置；也可以为用户生成的内容打上“位置标签”，比如标记照片的拍照位置。"
description: " 地理位置（Geolocation）API 能让你在用户允许情况下获取其位置信息。"
translator: <a href="http://crimx.com" target="_blank">黄杰华(StrayBugs)</a>
reviewer: （待校正）
article:
  written_on: 2014-06-06
  updated_on: 2014-08-01
  order: 1
rel:
  gplusauthor: https://plus.google.com/+PaulKinlan
  twitterauthor: "@Paul_Kinlan"
collection: user-location
key-takeaways:
  geo: 
    -  使用 API 前先检测兼容性
    -  粗略定位比精确定位好
    -  注意处理错误
    -  控制获取数据的频率以节省用户电量


---

{% wrap content %}

{% include modules/toc.liquid %}

{% include modules/takeaway.liquid list=page.key-takeaways.geo %}

这个 API 是设备无关的，它不管浏览器如何检测位置，只要用户能以标准方式请求和接收位置信息即可。底层可能是通过 GPS、wifi 甚至是让用户手动输入地址。这些查找都需要花费一定时间，所以这个 API 是异步的，在请求的时候要传回调函数。

## 地理位置的用处

*  为实际物理站点附近的用户提供私人定制的用户体验。
*  根据用户位置提供定制信息（比如新闻）。
*  在地图上显示用户位置。
*  在标签数据中嵌入用户的位置（比如照片的位置信息）。



## 检查兼容性

如今大多数浏览器都支持地理位置 API，但在使用前最好还是检查一下支持。

可以检测 `geolocation` 对象是否存在来测试兼容性。:

{% highlight javascript %}
// check for Geolocation support
if (navigator.geolocation) {
  console.log('Geolocation is supported!');
}
else {
  console.log('Geolocation is not supported for this Browser/OS version yet.');
}
{% endhighlight %}

## 检测用户当前位置

地理位置 API 提供了唯一的 `getCurrentPosition()` 函数来获取用户位置。调用此函数后会异步反馈用户当前的位置。

{% highlight javascript %}
window.onload = function() {
  var startPos;
  var geoSuccess = function(position) {
    startPos = position;
    document.getElementById('startLat').innerHTML = startPos.coords.latitude;
    document.getElementById('startLon').innerHTML = startPos.coords.longitude;
  };
  navigator.geolocation.getCurrentPosition(geoSuccess);
};
{% endhighlight %}

如果这是该域名下的应用第一次请求权限，浏览器一般会要求用户的允许。在一些浏览器上还可能会有“允许”或“不允许”的偏好配置，这时浏览器就会直接绕过用户确定。

根据浏览器使用的定位设备，位置对象还可能会包含经纬度以外的信息，比如海拔和方向。只有在定位系统返回数据的时候才能知道其包含的额外信息。

## 为网站测试地理位置功能

对于使用 HTML5 地理位置支持的应用，可以利用不同的经纬度数值进行调试。

Chrome 开发者工具支持重写 navigator.geolocation 位置数值以及模拟重写菜单不支持的地理位置。

<img src="images/emulategeolocation.png">

*  打开开发者工具额重写菜单
*  选择“重写地理位置”（Override Geolocation），然后输入 Lat = 41.4949819（纬度）和 Lon = -0.1461206（经度）
*  刷新页面应用重写的地理位置


##  注意处理错误

查找位置不一定成功；可能是 GPS 无法定位或者用户突然中止了位置查询。错误事件会调用 `getCurrentPosition()` 的第二个可选的参数，所以你可以在回调函数里告知用户:

{% highlight javascript %}
window.onload = function() {
  var startPos;
  var geoSuccess = function(position) {
    startPos = position;
    document.getElementById('startLat').innerHTML = startPos.coords.latitude;
    document.getElementById('startLon').innerHTML = startPos.coords.longitude;
  };
  var geoError = function(position) {
    console.log('Error occurred. Error code: ' + error.code);
    // error.code 可以是:
    //   0: 未知错误
    //   1: 权限不足
    //   2: 位置错误(位置供应商出错)
    //   3: 超时
  };
  navigator.geolocation.getCurrentPosition(geoSuccess, geoError);
};
{% endhighlight %}

## 减少启动地理定位的硬件需要

许多情况下我们不需要用户最新的位置，只需一个粗略的估值。

利用 `maximumAge` 可选属性可以告知浏览器使用最近一次获取的位置结果。这不仅在用户已经请求过数据的情况下响应更快，而且不必启动地理位置硬件接口比如 Wifi 三角定位或 GPS。

{% highlight javascript %}
window.onload = function() {
  var startPos;
  var geoOptions = {
  	maximumAge: 5 * 60 * 1000,
  }

  var geoSuccess = function(position) {
    startPos = position;
    document.getElementById('startLat').innerHTML = startPos.coords.latitude;
    document.getElementById('startLon').innerHTML = startPos.coords.longitude;
  };
  var geoError = function(position) {
    console.log('Error occurred. Error code: ' + error.code);
    // error.code 可以是:
    //   0: 未知错误
    //   1: 权限不足
    //   2: 位置错误(位置供应商出错)
    //   3: 超时
  };

  navigator.geolocation.getCurrentPosition(geoSuccess, geoError, geoOptions);
};
{% endhighlight %}

## 设置超时以避免用户等待过长

没有设置超时的话，位置请求有可能永远都不返回。

{% highlight javascript %}
window.onload = function() {
  var startPos;
  var geoOptions = {
     timeout: 10 * 1000
  }

  var geoSuccess = function(position) {
    startPos = position;
    document.getElementById('startLat').innerHTML = startPos.coords.latitude;
    document.getElementById('startLon').innerHTML = startPos.coords.longitude;
  };
  var geoError = function(error) {
    console.log('Error occurred. Error code: ' + error.code);
    // error.code 可以是:
    //   0: 未知错误
    //   1: 权限不足
    //   2: 位置错误(位置供应商出错)
    //   3: 超时
  };

  navigator.geolocation.getCurrentPosition(geoSuccess, geoError, geoOptions);
};
{% endhighlight %}

## 粗略定位比精确定位好

如果你只是需要知道离用户最近的存储点，则没必要获取1米的精度。设置这个 API 是为了尽快获取粗略定位。

如果你需要请求高精度，可以重写 `enableHighAccuracy` 的默认设置。请谨慎使用：它会减慢解析速度并消耗更多电量。

{% highlight javascript %}
window.onload = function() {
  var startPos;
  var geoOptions = {
    enableHighAccuracy: true
  }

  var geoSuccess = function(position) {
    startPos = position;
    document.getElementById('startLat').innerHTML = startPos.coords.latitude;
    document.getElementById('startLon').innerHTML = startPos.coords.longitude;
  };
  var geoError = function(error) {
    console.log('Error occurred. Error code: ' + error.code);
    // error.code 可以是:
    //   0: 未知错误
    //   1: 权限不足
    //   2: 位置错误(位置供应商出错)
    //   3: 超时
  };

  navigator.geolocation.getCurrentPosition(geoSuccess, geoError, geoOptions);
};
{% endhighlight %}


{% endwrap %}
