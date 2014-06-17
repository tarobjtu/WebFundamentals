---
layout: article
title: "Obtain the user's location"
introduction: "The Geolocation API lets you find out where the user is and
keep tabs on them as they move around, always with the user's consent. This
functionality could be used as part of user queries, e.g. to guide someone to
a destination point. It could also be used for 'geo-tagging' some content the
user has created, e.g. to mark where a photo was taken."
description: "The Geolocation API lets you find out where the user is and keep tabs on them as they move around, always with the user's consent."
article:
  written_on: 2014-01-01
  updated_on: 2014-01-06
  order: 1
rel:
  gplusauthor: https://plus.google.com/+PaulKinlan
collection: user-location
key-takeaways:
  geo: 
    -  Check for Compatibility before you use the API
    -  Prefer a coarse location, over a fine location
    -  Always handle errors
    -  Don't poll for the data too frequently to save the user's battery

---

{% wrap content %}

{% include modules/toc.liquid %}

{% include modules/takeaway.liquid list=page.key-takeaways.geo %}

The API is device-agnostic; it doesn't care how the browser determines
location, so long as clients can request and receive location data in a
standard way. The underlying mechanism might be via GPS, wifi, or simply
asking the user to enter their location manually. Since any of these lookups
is going to take some time, the API is asynchronous; you pass it a callback
method whenever you request a location.

## Check for Compatibility

The geolocation API is now supported in the majority of browsers, but it is
good practice to always check for support before you do anything.

You can easily check for compatibility by testing for the presence of the
geolocation object:

{% highlight javascript %}
// check for Geolocation support
if (navigator.geolocation) {
  console.log('Geolocation is supported!');
}
else {
  console.log('Geolocation is not supported for this Browser/OS version yet.');
}
{% endhighlight %}

## Determine the User's Current Location

The geolocation API offeres a simple 'one-shot' method to obtain the users
location  `getCurrentPosition()`.  A call to this method will asynchronously
report on the user's  current location.

{% highlight javascript %}
window.onload = function() {
  var startPos;
  navigator.geolocation.getCurrentPosition(function(position) {
    startPos = position;
    document.getElementById('startLat').innerHTML = startPos.coords.latitude;
    document.getElementById('startLon').innerHTML = startPos.coords.longitude;
  });
};
{% endhighlight %}

If this is the first time an application on this domain has requested
permissions, the browser will typically check for user consent. Depending on
the browser, there may also be preferences to always allow - or disallow -
permission lookups, in which case the confirmation process will be bypassed.

Depending on the location device your browser is using, the position object
might actually contain a lot more than just latitude and longitude, e.g. it
could include an altitude or a direction.  You can't tell what extra information
that location system will use until it actually returns the data.

## Testing Geolocation with your site

When working with HTML5 geolocation support in an application, it can be
useful to debug the output received when using different values for longitude
and latitude.

The DevTools support both overriding position values for navigator.geolocation
and simulating geolocation not being available via the overrides menu.

<img src="images/emulategeolocation.png">

*  Open up the overrides menu in the DevTools
*  Check “Override Geolocation” then enter in Lat = 41.4949819 and Lat = -0.1461206
*  Refresh the page and it will now use your overridden positions for geolocation

## Decide how accuratly you need the location

TODO: Note - Fused Location

## Set a timeout

##  Handle Errors

Unfortunately, not all location lookups are successful. Perhaps a GPS could
not be located or the user has suddenly disabled location lookups. A second,
optional, argument to getCurrentPosition() will be called in the event of an
error, so you can notify the user inside the callback:

{% highlight javascript %}
window.onload = function() {
  var startPos;
  navigator.geolocation.getCurrentPosition(function(position) {
    // same as above
  }, function(error) {
    alert('Error occurred. Error code: ' + error.code);
    // error.code can be:
    //   0: unknown error
    //   1: permission denied
    //   2: position unavailable (error response from locaton provider)
    //   3: timed out
  });
};
{% endhighlight %}

{% endwrap %}