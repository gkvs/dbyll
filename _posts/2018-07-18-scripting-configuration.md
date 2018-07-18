---
layout: post
title: Scripting Configuration
categories: [lua, script, configuration]
tags: [lua, script, configuration]
fullview: true
comments: true
---

GKVS designed to support startup initialization and remote config.
For this purpose it uses scripting configuration based on Lua language.

It gives flexibility to setup endpoints and change confguration on the fly.

Example of Aerospike endpoint:
{% highlight ruby %}
config = {

    hosts = {
      {
        host="192.168.56.101",
        port=3000
      }
    },
    user="",
    password=""
}

add_cluster("as1", "aerospike", config );

add_table("test", "as1", { namespace="test", ttl = 100 } );

add_view("TEST", {cluster = "as1", table = "test" });
{% endhighlight %}

Example of Redis endpoint:
{% highlight ruby %}
add_cluster("redis1", "redis", { host = "127.0.0.1", port = 6379 } );

add_table("test", "redis1", { ttl = 100 } );

add_view("TEST", { cluster="redis1", table="test" } );
{% endhighlight %}

Only *views* are visible for the client. So, in this case we always can *redirect* view to another table runtime.
