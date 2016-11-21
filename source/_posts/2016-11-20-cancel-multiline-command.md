---
layout: post
title:  "Cancel a multiline command"
keywords: "iex"
category: "IEx"
comments: true
---

When typing multiline commands into IEx it is easy to get lost in opening and
closing symbols. For those cases you can issue `#iex:break` to interrupt the
declaration of that command. For example:

{% highlight elixir %}
iex> IO.puts "hello world
...>
...> #iex:break
** (TokenMissingError) iex:1: incomplete expression
iex>
{% endhighlight %}

**Additional reading:**
- [Elixir interactive shell](http://elixir-lang.org/docs/stable/iex/IEx.html)
