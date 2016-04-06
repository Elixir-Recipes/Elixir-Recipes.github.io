---
layout: post
title:  "Debug tracing"
keywords: "processes, debug, trace, sys"
category: "concurrency"
comments: true
---

Use `:sys` methods to get more information about your servers. You can use:

- `:sys.trace`
- `:sys.get_status`
- `:sys.statistics`

Optionally, you can turn on debug mode by specifying the `debug` parameter in a `GenServer` `start_link` call:

{% highlight elixir %}
iex> {:ok, pid} = GenServer.start_link(MyModule.Server, %{}, [debug: [:statistics, :trace]])
{% endhighlight %}

You can also enable tracing on an existing server using:

{% highlight elixir %}
iex> :sys.trace pid, true
{% endhighlight %}

With debug turned on, you get a trace of messages:

{% highlight elixir %}
iex> GenServer.call(pid, :my_command)
*DBG* <0.77.0> got call :my_command from<0.55.0>
*DBG* <0.77.0> sent %{} to <0.55.0>, new state %{}
{% endhighlight %}



