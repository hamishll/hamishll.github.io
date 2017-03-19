---
layout: post
title: findapcfor.me
cover: cover_findapcforme.png
date:   2017-03-19 12:00:00
categories: posts
---

## Introduction

[findapcfor.me](http://findapcfor.me) is a web app for finding available computers at The University of Manchester. It uses AJAX alongside the Google Maps API in order to map...

The university tracks the status of PC clusters in an XML table, hosted [here](http://www.itservices.manchester.ac.uk/clusteravailability/avail.php). Each location is described something like this:

{% highlight XML %}
<PLPlace>
   <name>AGLC Floor -1</name>
   <description />
   <open>true</open>
   <latitude>53.464630</latitude>
   <longitude>-2.233479</longitude>
   ...
   <locationCode>010AA</locationCode>
   <locationName>Alan Gilbert Learning Commons</locationName>
   <availability>29 seats taken, 31 seats available</availability>
</PLPlace>
{% endhighlight %}

## Pulling the XML document (AJAX)

We'll use AJAX to request this file. Below is a basic function to achieve this:

{% highlight js %}
function downloadUrl(url,callback) {
    var request = window.ActiveXObject ?
         new ActiveXObject('Microsoft.XMLHTTP') :
         new XMLHttpRequest;
     
    request.onreadystatechange = function() {
        if (request.readyState == 4) {
            //request.onreadystatechange = doNothing;
            callback(request, request.status);
        }
    };
     
    request.open('GET', url, true);
    request.send(null);
}
{% endhighlight %}

We can then call each row in the table by refering to the DOM and using the getElementsByTagName method. For example:

{% highlight js %}
	var name = markers[i].getElementsByTagName("name")[0].innerHTML;
{% endhighlight %}

## Styling markers based on availability

What we want to achieve is a gradient

## Check out the code on GitHub

[findapcfor.me on GitHub](http://github.com/hamishll/findapcfor.me)
