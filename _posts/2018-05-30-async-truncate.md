---
layout: post
title:  Async truncate table
categories: [api, java, client]
tags: [gkvs, java, client, cleanup]
fullview: true
comments: true
---

There is an async was to truncate table by scanning all record and sending all keys to remove.

{% highlight java %}
Observer<Key> key = Gkvs.Client.removeAll().async(Observers.<Status>console(done));				
Observer<Record> record = Observers.transform(key, Observers.GET_KEY_FN);
Gkvs.Client.scan(TABLE).async(record);
{% endhighlight %}    
    
