---
layout: post
title:  "Capturing functions"
keywords: "functions, anonymous functions, capture functions"
category: "functions"
comments: true
---

Use `&` to capture functions from other modules. You can use the captured functions directly as function parameters or within anonymous functions.

Compare the two programs below:

{% highlight elixir %}
Enum.map(list, fn(x) -> String.capitalize(x) end)
{% endhighlight %}

{% highlight elixir %}
Enum.map(list, &String.capitalize(&1))
{% endhighlight %}

Capturing functions without passing any arguments require you to explicitly specify its arity, e.g. `&String.capitalize/1`:

{% highlight elixir %}
defmodule Bob do
  def say(message, f \\ &String.capitalize/1) do
    f.(message)
  end
end
{% endhighlight %}