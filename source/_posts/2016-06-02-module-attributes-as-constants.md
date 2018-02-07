---
layout: post
title:  "Module attributes as constants"
keywords: "module, constants"
category: "modules"
comments: true
---

Use the `@` symbol to create module attributes, which can then be used as constants
by functions in your module:

{% highlight elixir %}
defmodule Robot do
  @name "R080T"

  def greet do
    IO.puts "Greetings from #{@name}!"
  end
end
{% endhighlight %}
