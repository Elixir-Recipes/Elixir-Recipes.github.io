---
layout: post
title:  "Pipelining operations"
keywords: "pipe, flow control"
category: "flow control"
comments: true
---

The `|>` (pipe) operator introduces the expression on the left-hand side as the first argument to the function call on the right-hand side. True to functional programming, we treat our programs as a series of data transformations.

{% highlight elixir %}
nums = [1,[2],3]
nums
|> List.flatten()
|> Enum.map(fn x -> x * 2 end)
{% endhighlight %}

The above is equivalent to:

{% highlight elixir %}
Enum.map(List.flatten([1, [2], 3]), fn x -> x * 2 end)
{% endhighlight %}

The above code appears in reverse order, where earlier operations are inner expressions. We have to start from the middle and read outwards to understand the sequence.
Using pipes leads to a clearer sequence of operations.

Here's another example taken from the [Ecto](https://github.com/elixir-lang/ecto/blob/master/lib/ecto/migration.ex) database wrapper:

{% highlight elixir %}
defp default_index_name(index) do
  [index.table, index.columns, "index"]
  |> List.flatten()
  |> Enum.join("_")
  |> String.replace(~r"[^\w_]", "_")
  |> String.replace("__", "_")
  |> String.to_atom()
end
{% endhighlight %}

**Additional reading:**

- [Pipe operator](http://elixir-lang.org/docs/stable/elixir/Kernel.html#%7C%3E/2)
