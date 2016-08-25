---
layout: post
title:  "Configuration"
keywords: "configuration"
category: "mix"
comments: true
---

You can specify `config` values for the current project and its third-party dependencies at `config/config.exs`:

{% highlight elixir %}
# config/config.exs
use Mix.Config

# Project config
config :mymodule,
  api_url: "http://api.seave.co"
  namespace: "hello"

# Third party dependency
config :logger,
  verbose: true
{% endhighlight %}

Your current project and any third party libraries will be able to pick it up through `Application.get_env`:

{% highlight elixir %}
# lib/client.exs

defmodule Client do
  def log
    IO.puts Application.get_env(:mymodule, :key)
  end
end

iex> Client.log
hello
{% endhighlight %}
