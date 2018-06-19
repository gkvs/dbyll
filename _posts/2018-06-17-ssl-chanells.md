---
layout: post
title: SSL channels
categories: [C++, java, SSL, TLS, security, certstrap, openssl]
tags: [SSL, TLS, C++, java, security, certstrap, openssl]
fullview: true
comments: true
---

Since last updage of GKVS all connections and channels beween clients ans servers are protected by SSL/TLS.
gRPC has the option to leverage SSL in protocol, that option is enforced for GKVS. because Generic Key Value Service 
is intended to transfer raw data between clients and servers.

### How to configure

GKVS has a special module *gkvs-keys*. 
<a class="btn btn-default" href="https://github.com/gkvs/gkvs-keys">Grab your copy now!</a>

Quick start steps:
* download *gkvs-keys*
* install *certstrap*
* run bootstrap.sh scrypt
* setup GKVS_KEYS env

### Certstrap

Certstrap is not required, but simplifies keys/certs generation. All operations you can do by using *OpenSSL*.
<a class="btn btn-default" href="https://github.com/square/certstrap">Grab your copy now!</a>

### Performance

*GKVS* showed good and acceptable results on peformance tests with enforced SSL. 
GKVS-java-client has a native implementation of SSL security provider, so makes Java really good on this.

Performance test:
{% highlight java %}
for (int i = 0; i != 10000; ++i) {
	String key = UUID.randomUUID().toString();
	Gkvs.Client.put(TABLE, key, "value").sync();
	Gkvs.Client.get(TABLE, key).sync().value();
	Gkvs.Client.remove(TABLE, key);
}
{% endhighlight %}

Showed good results with enforced SSL:
{% highlight ruby %}
30000 requests in 10132 milliseconds, 0.33773333333333333
{% endhighlight %}

That makes *GKVS* a good candidate for enterprise solutions.
