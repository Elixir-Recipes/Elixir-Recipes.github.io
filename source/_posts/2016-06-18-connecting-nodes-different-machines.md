---
layout: post
title:  "Connecting nodes on different machines"
keywords: "nodes, connect"
category: "concurrency"
comments: true
---

Let's see how we can connect multiple nodes on the same machine:

{% highlight bash %}
$ iex --sname foo
iex(foo@yosriady)> Node.list
[]
{% endhighlight %}

{% highlight bash %}
$ iex --sname bar
iex(bar@yosriady)> Node.list
[]
{% endhighlight %}

We have two nodes, both unaware of each other. Let's connect them:

{% highlight elixir %}
iex(foo@yosriady)> Node.ping :"bar@yosriady"
:pong # returns :pang if ping failed
iex(foo@yosriady)> Node.list
[:"bar@yosriady"]
{% endhighlight %}

{% highlight elixir %}
iex(bar@yosriady)> Node.list
[:"foo@yosriady"]
{% endhighlight %}

Both nodes are now aware of each other!

Now let's see how we can connect multiple nodes on different machines over the network. You'll need to get the two machines' IP addresses via `ifconfig`:

{% highlight bash %}
$ ifconfig
lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
	options=3<RXCSUM,TXCSUM>
	inet6 ::1 prefixlen 128
	inet 127.0.0.1 netmask 0xff000000
	inet6 fe80::1%lo0 prefixlen 64 scopeid 0x1
	nd6 options=1<PERFORMNUD>
gif0: flags=8010<POINTOPOINT,MULTICAST> mtu 1280
stf0: flags=0<> mtu 1280
en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
	ether 34:36:3b:d4:fc:dc
	inet6 fe80::3636:3bff:fed4:fcdc%en0 prefixlen 64 scopeid 0x4
	inet 10.238.82.82 netmask 0xfffffe00 broadcast 10.238.83.255
	nd6 options=1<PERFORMNUD>
	media: autoselect
	status: active
{% endhighlight %}

From the above, my IP address is `10.238.82.82`. My other machine has IP `10.238.82.85`:

{% highlight elixir %}
$ iex --name foo@10.238.82.82 --cookie chocolate
iex(foo@10.238.82.82)> Node.ping :"bar@10.238.82.85"
:pong
iex(foo@10.238.82.82)> Node.list
[:"bar@10.238.82.85"]
{% endhighlight %}

{% highlight elixir %}
$ iex --name bar@10.238.82.85 --cookie chocolate
iex(bar@10.238.82.85)> Node.list
[:"foo@10.238.82.82"]
{% endhighlight %}
