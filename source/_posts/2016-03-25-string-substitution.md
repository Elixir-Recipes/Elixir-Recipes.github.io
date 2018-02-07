---
layout: post
title:  "String substitution"
keywords: "string, substitution, interpolation"
category: strings
comments: true
---

You can perform string substitution using `#{}`

{% highlight elixir %}
iex> name = "José"
iex> IO.puts("Hello, #{name}!")
Hello, José!
:ok
{% endhighlight %}