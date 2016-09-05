---
layout: post
title: "Trim whitespace from strings"
kewyords: "trim, whitespace"
category: strings
comments: true
---

Using `String.strip`, `String.lstrip`, and `String.rstrip` to trim whitespace from strings:

{% highlight elixir %}
iex> String.strip("   abc  ")
"abc"
{% endhighlight %}
