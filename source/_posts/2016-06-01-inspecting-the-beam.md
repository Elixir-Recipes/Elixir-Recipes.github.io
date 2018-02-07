---
layout: post
title:  "Inspecting the BEAM"
keywords: "BEAM, inspect, "
category: "performance"
comments: true
---

{% highlight elixir %}
iex> :observer.start
:ok
{% endhighlight %}

This will open the GUI observer interface, showing you CPU breakdown, memory usage, and other information critical to understanding the usage patterns of your applications.
