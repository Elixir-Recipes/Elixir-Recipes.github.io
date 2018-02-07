---
layout: post
title:  "Default function parameters"
keywords: "functions, default parameters, optional parameters"
category: functions
comments: true
---

Specify default values for your function parameters using `\\`:

{% highlight elixir %}
defmodule Bob do
  def say(message \\ "Hi, I'm Bob!") do
    "Bob says: #{message}"
  end	
end
{% endhighlight %}

{% highlight elixir %}
iex> Bob.say
"Bob says: Hi, I'm Bob!"
iex> Bob.say "Morning!"
"Bob says: Morning!"
{% endhighlight %}

> Do be careful if you're using optional parameters when definining functions of the same name but different arity. Since named functions in Elixir are identified by its name and arity, optional parameters can lead to some ambiguity. Elixir will warn you if your function definitions conflict.