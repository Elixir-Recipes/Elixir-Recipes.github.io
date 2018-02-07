---
layout: post
title:  "Microbenchmarking"
keywords: "performance, benchmarking"
category: "performance"
comments: true
---

Use [`benchfella`](https://github.com/alco/benchfella) or [`benchee`](https://github.com/PragTob/benchee) to perform microbenchmarking of your Elixir code.

Using `benchfella`:

{% highlight elixir %}
defmodule BasicBench do
  use Benchfella

  @list Enum.to_list(1..1000)

  bench "hello list" do
    Enum.reverse @list
  end
end
{% endhighlight %}

Using `benchee`:

{% highlight elixir %}
list = Enum.to_list(1..10_000)
map_fun = fn(i) -> [i, i * i] end

Benchee.run(%{time: 3}, %{
  "flat_map"    => fn -> Enum.flat_map(list, map_fun) end,
  "map.flatten" => fn -> list |> Enum.map(map_fun) |> List.flatten end})
{% endhighlight %}
