---
layout: post
title: Performance tests
categories: [aerospike, redis]
tags: [aerospike, redis]
fullview: true
comments: true
---

CRUID performance tests on the same machine:

Redis
{% highlight ruby %}
30000 requests in 6813 milliseconds, 0.2271
{% endhighlight %}

Aerospike
{% highlight ruby %}
30000 requests in 9820 milliseconds, 0.3273333333333333
{% endhighlight %}

RocksDB 
{% highlight ruby %}
30000 requests in 7446 milliseconds, 0.2482
{% endhighlight %}

Performance test code
{% highlight java %}
		long t0 = System.currentTimeMillis();
		
		for (int i = 0; i != 10000; ++i) {
			String key = UUID.randomUUID().toString();
			Gkvs.Client.put(TEST, key, new Str("value")).sync();
			Gkvs.Client.get(TEST, key).sync().value();
			Gkvs.Client.remove(TEST, key);
		}
		
		long diff = System.currentTimeMillis() - t0;
		
		System.out.println("30000 requests in " + diff + " milliseconds, " + (double) diff / 30000.0);
{% endhighlight %}
