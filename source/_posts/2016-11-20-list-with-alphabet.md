---
layout: post
title:  "Create an array containing the alphabet"
keywords: "comprehensions, code points, char list"
category: "strings"
comments: true
---

A charlist containing the alphabet can be obtained by doing the following:

{% highlight elixir %}
iex> for n <- ?a..?z, do: n
'abcdefghijklmnopqrstuvwxyz'
{% endhighlight %}

Alternatively, since ranges i.e `?a..?z` implement the [`Enumerable`](https://hexdocs.pm/elixir/Enumerable.html) protocol, you can also
generate the charlist by converting the range to a list:

{% highlight elixir %}
iex> Enum.to_list(?a..?z)
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
- [Comprehensions](https://elixir-lang.org/getting-started/comprehensions.html)
- [Enum](https://hexdocs.pm/elixir/Enum.html)
- [Range](https://hexdocs.pm/elixir/Range.html)
