---
layout: post
title:  "Using Erlang from Elixir"
keywords: "interop, erlang"
category: "erlang"
comments: true
---

Erlang modules are available as `atoms`, for example the Erlang `math` module is available as `:math`:

{% highlight elixir %}
iex> :math.pi
3.141592653589793
{% endhighlight %}
