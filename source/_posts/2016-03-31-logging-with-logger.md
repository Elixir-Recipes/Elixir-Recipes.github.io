---
layout: post
title:  "Logging with Logger"
keywords: "logging"
category: "logging"
comments: true
---

To generate logs:

{% highlight elixir %}
Logger.info "Completed operation A"
Logger.debug fn -> inspect(somevar) end
Logger.error "Some exception #{somexception} occured"
{% endhighlight %}

For projects generated with `Mix`, you can specify some options in `config/config.exs`:


{% highlight elixir %}
use Mix.Config
config :logger, 
  backends: [:console] # default, support for additional log sinks
  compile_time_purge_level: :info # purges logs with lower level than this
{% endhighlight %}

> A full range options are available in the official [Logger](http://elixir-lang.org/docs/stable/logger/Logger.html) documentation.


**Additional reading:**

- [Logger](http://elixir-lang.org/docs/stable/logger/Logger.html)