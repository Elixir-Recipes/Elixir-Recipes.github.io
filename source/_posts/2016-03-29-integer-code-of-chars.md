---
layout: post
title:  "Integer code of a character"
keywords: "char, character, code"
category: "characters"
comments: true
---

Single-quoted strings in Elixir are represented by a list of integer values, each value representing a character.

Get the integer code of a character using `?`:

{% highlight elixir %}
iex> ?a
97
iex> ?8
56
iex> ?+
43
{% endhighlight %}
