---
layout: post
title:  "Build lists with sigils"
keywords: "sigils, collections, strings"
category: "collections"
comments: true
---

Use the `~w` sigil to generate lists of strings:

{% highlight elixir %}
iex> ~w(a b c)
["a", "b", "c"]
{% endhighlight %}

Append the `a` option to generate a list of atoms:

{% highlight elixir %}
iex> ~w(a b c)a
[:a, :b, :c]
{% endhighlight %}
