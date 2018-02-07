---
layout: post
title:  "Slicing a string"
keywords: "strings, slice"
category: "strings"
comments: true
---

{% highlight elixir %}
iex> my_string = "Lorem ipsum dolor sit amet, consectetur adipiscing elit."
iex> String.slice my_string, 6..10
"ipsum"
{% endhighlight %}
