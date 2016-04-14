---
layout: post
title:  "Option parameters with keyword lists"
keywords: "functions, keyword list"
category: "functions"
comments: true
---

Use keyword lists for 'options'-style parameters that contains multiple key value pairs:

{% highlight elixir %}
def myfunc(arg1, opts \\ []) do
  # Function body
end
{% endhighlight %}

We can call the function above like so:

{% highlight elixir %}
iex> myfunc "hello", pizza: true, soda: false
{% endhighlight %}

which is equivalent to:
{% highlight elixir %}
iex> myfunc("hello", [pizza: true, soda: false])
{% endhighlight %}

The argument values are available as `opts.pizza` and `opts.soda` respectively.

[Ecto](https://hexdocs.pm/ecto/Ecto.Query.html#from/2)'s query language uses this pattern:

{% highlight elixir %}
query = from p in EctoBlog.Post, where: p.id == post_id
{% endhighlight %}

You can probably guess by now, but the above code is actually:

{% highlight elixir %}
query = from(p in EctoBlog.Post, [where: p.id == 1])
{% endhighlight %}

Yes, the second parameter of the `from` function is a keyword list.