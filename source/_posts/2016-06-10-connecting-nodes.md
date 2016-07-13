---
layout: post
title:  "Connecting nodes"
keywords: "nodes, concurrency"
category: "concurrency"
comments: true
---

Start two named nodes in two terminal windows:

{% highlight elixir %}
>iex --name bob@127.0.0.1
iex(bob@127.0.0.1)>
{% endhighlight %}

{% highlight elixir %}
>iex --name frank@127.0.0.1
iex(frank@127.0.0.1)>
{% endhighlight %}

Connect two nodes by instructing one node to `connect`:

{% highlight elixir %}
iex(bob@127.0.0.1)> Node.connect :"frank@127.0.0.1"
true
{% endhighlight %}

The two nodes are now connected and aware of each other:

{% highlight elixir %}
iex(bob@127.0.0.1)> Node.list
[:"frank@127.0.0.1"]
iex(frank@127.0.0.1)> Node.list
[:"bob@127.0.0.1"]
{% endhighlight %}

You can execute code on other nodes:

{% highlight elixir %}
iex(bob@127.0.0.1)> greet = fn() -> IO.puts("Hello from #{inspect(Node.self)}") end
iex(bob@127.0.0.1)> Node.spawn(:"frank@127.0.0.1", greet)
#PID<9007.74.0>
Hello from :"frank@127.0.0.1"
:ok
{% endhighlight %}
