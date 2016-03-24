---
layout: post
title:  "Parallel Map"
keywords: "parallel, collection, enumeration, map"
category: concurrency
comments: true
---

We define an Elixir function `pmap` using the [Task API](http://elixir-lang.org/docs/stable/elixir/Task.html) to convert sequential code into concurrent code by computing values asynchronously:

{% highlight elixir %}
defmodule Parallel do
  def pmap(collection, func)
    collection
    |> Enum.map(&(Task.async(fn -> func.(&1 end))))
    |> Enum.map(&Task.await/1)
  end
end
{% endhighlight %}

We can run this function to get the squares of numbers from 1 to 10000:

{% highlight elixir %}
iex(1)> c("parallel.ex")
iex(2)> res = Parallel.pmap 1..10000, &(&1 * &1)
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100, 121, 144, 169, 196, 225, 256, 289, 324,
 361, 400, 441, 484, 529, 576, 625, 676, 729, 784, 841, 900, 961, 1024, 1089,
 1156, 1225, 1296, 1369, 1444, 1521, 1600, 1681, 1764, 1849, 1936, 2025, 2116,
 2209, 2304, 2401, 2500, ...]
{% endhighlight %}

In the background, we've spawned 10000 processes to perform the same squaring operation on multiple data points simultaneously. We make use of all the cores and processors on our machine.