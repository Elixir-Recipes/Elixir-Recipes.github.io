---
layout: post
title:  "Anonymous functions"
keywords: "functions, lambdas, anonymous functions"
category: functions
comments: true
---

You can define anonymous functions using `fn`:

{% highlight elixir %}
iex> multiply = fn (x,y) -> x + y end
iex> multiply.(2,3)
6
{% endhighlight %}

You can use `&` for shorthand form, where `&N` refers to the `N`-th parameter:

{% highlight elixir %}
iex> multiply = &(&1 * &2)
iex> multiply.(2,3)
6
{% endhighlight %}


Functions can have multiple clauses using pattern matching:

{% highlight elixir %}
fn
  {:ok, result} -> "Success: #{result}"
  {_, error} -> "Error: #{error}"
end
{% endhighlight %}
