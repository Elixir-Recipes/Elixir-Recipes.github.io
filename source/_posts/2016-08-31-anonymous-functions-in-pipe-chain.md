---
layout: post
title: "Anonymous functions in pipe chain"
kewyords: "lambda, pipe"
category: functions
comments: true
---

Insert anonymous functions into your pipe chains by defining and applying the function like so:

{% highlight elixir %}
  def md5(str) do
    str
    |> (fn(s) -> :erlang.md5(s) end).()
    |> Base.encode16(case: :lower)
  end
{% endhighlight %}

Alternatively:

{% highlight elixir %}
  def md5(str) do
    str
    |> (&(:erlang.md5(&1))).()
    |> Base.encode16(case: :lower)
  end
{% endhighlight %}
