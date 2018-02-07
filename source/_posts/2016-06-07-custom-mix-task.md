---
layout: post
title:  "Custom Mix Task"
keywords: "mix, task"
category: "mix"
comments: true
---

Create a custom `mix` task:

{% highlight elixir %}
# lib/mix/tasks/mytask.ex
defmodule Mix.Tasks.MyTask do
  use Mix.Task

  @shortdoc "A simple mix task"
  def run(_) do
    IO.puts "YO!"
  end
end
{% endhighlight %}

Compile and run it:

{% highlight bash %}
> mix compile
> mix my_task
"YO!"
{% endhighlight %}

> `mix help` lists out all available mix tasks for the project.
