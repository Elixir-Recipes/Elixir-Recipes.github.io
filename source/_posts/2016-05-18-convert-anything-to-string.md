---
layout: post
title:  "Convert anything to string"
keywords: "string, conversion"
category: "strings"
comments: true
---

Use `Kernel.inspect` to convert anything to `string`.

{% highlight elixir %}
iex> Kernel.inspect(1)
"1"
iex> Kernel.inspect(4.2)
"4.2"
iex(3)> Kernel.inspect %{pi: 3.14, name: "Yos"}
"%{pi: 3.14, name: \"Yos\"}"
{% endhighlight %}