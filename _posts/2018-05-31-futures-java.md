---
layout: post
title: Futures in Java
categories: [api, java, async]
tags: [gkvs, java, async]
fullview: true
comments: true
---

Future is the class in JDK that gives ability to get result somehow in the future. 
During the interval application can perform another task that how parallelism can give immediate benifit without deep refactoring of the application.

Here is the example of the GET with futures:
{% highlight java %}
GkvsFuture<Record> future = Gkvs.Client.get(KEY).async();
// do something else
Record record = future.getUnchecked(); // blocking code 
{% endhighlight %}

And MULTI_GET example:
{% highlight java %}
GkvsFuture<Iterable<Record>> records = Gkvs.Client.multiGet(LOAD_KEYS).async();

// do something else

for (Record rec : records.getUnchecked()) {
		System.out.println(rec.key().get());
}
{% endhighlight %}

**GkvsFuture** also supports classical get() function with all checked exceptions in the list.

Additionally *GkvsFuture* has ability to register a listener and get notification when data will be available.

Listener example:
{% highlight java %}
final AtomicBoolean triggered = new AtomicBoolean(false);
GkvsFuture<Record> future = Gkvs.Client.get(KEY).async();

future.addListener(new Runnable() {

	@Override
	public void run() {
			triggered.set(true);
	}
			
});
{% endhighlight %}
