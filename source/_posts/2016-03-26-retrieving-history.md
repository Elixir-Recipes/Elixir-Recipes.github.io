---
layout: post
title:  "Retrieving values from history"
keywords: "history"
category: "IEx"
comments: true
---

You can use the `v` helper macro to get values from your `IEx` history.

{% highlight elixir %}
iex(1)> a = 1
1
iex(2)> b = 2
2
iex(3)> a + b
3
iex(4)> v(-1) # Retrives expression values relative to the current one 
3
iex(5)> v(2) # Retrieves expression values using an absolute index
2



{% endhighlight %}