---
layout: post
title:  "Project configuration"
keywords: "configuration, config"
category: "mix"
comments: true
---

For projects generated with `Mix`, you can specify configuration variables in `config/config.exs`

{% highlight elixir %}
use Mix.Config
config :redis, redis_url: "https://google.com"
{% endhighlight %}

In your code, you can retrieve this value like so:

{% highlight elixir %}
Application.get_env(:redis, :redis_url)
{% endhighlight %}

If you have environment specific config files, use `Mix.env`: 

{% highlight elixir %}
use Mix.Config
import_config "#{Mix.env}.exs"
{% endhighlight %}

**Additional reading:**

- [Mix.Config](http://elixir-lang.org/docs/stable/mix/Mix.Config.html)