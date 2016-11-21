---
layout: post
title:  "Create an array containing the alphabet"
keywords: "comprehensions, code points, char list"
category: "strings"
comments: true
---

A char list containing the alphabet can be obtained by doing the following:

{% highlight elixir %}
iex> for n <- ?a..?z, do: n
'abcdefghijklmnopqrstuvwxyz'
{% endhighlight %}

If desired, we can pass each bitcode to a binary to represent each letter as a
string:

{% highlight elixir %}
iex> for n <- ?a..?z, do: << n :: utf8 >>
["a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p",
"q", "r", "s", "t", "u", "v", "w", "x", "y", "z"]
{% endhighlight %}

**Additional reading:**
- [Binaries, strings, and char lists](http://elixir-lang.org/getting-started/binaries-strings-and-char-lists.html)
