---
layout: post
title: Performance tests 100k
categories: [aerospike, redis]
tags: [aerospike, redis]
fullview: true
comments: true
---

Performance tests with big payload (100k):

Redis
{% highlight ruby %}
30000 requests in 20540 milliseconds, 0.6846666666666666
{% endhighlight %}

Aerospike
{% highlight ruby %}
30000 requests in 24860 milliseconds, 0.8286666666666667
{% endhighlight %}

RocksDB 
{% highlight ruby %}
30000 requests in 52506 milliseconds, 1.7502
{% endhighlight %}

Performance test payload generator
{% highlight java %}
	private String genval(int chars) {
		StringBuilder str = new StringBuilder();
		for (int i = 0; i != chars; ++ i) {
			str.append('a');
		}
		return str.toString();
	}
{% endhighlight %}
