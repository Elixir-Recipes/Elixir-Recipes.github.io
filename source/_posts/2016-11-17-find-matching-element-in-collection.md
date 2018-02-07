---
layout: post
title:  "Finding matching elements in a list or a map"
keywords: "find, list, map, pattern matching"
category: collections
comments: true
---

When storing data in lists or maps in Elixir we can use pattern matching to
access the elements of those collections easily.

Below are a few ways of how to do it.

{% highlight elixir %}
defmodule Find do
  @moduledoc """
  Implements methods to find elements in given collections by pattern matching.
  """

  @doc """
  Finds the first element in a list to match a given pattern.
  """
  def first_match(collection) do
    Enum.find(collection, fn(element) ->
      match?({:fruit, _}, element)
    end)
  end

  @doc """
  Finds all the elements in a list that match a given pattern.
  """
  def all_matches(collection) do
    Enum.filter(collection, fn(element) ->
      match?({:fruit, _}, element)
    end)
  end
end
{% endhighlight %}

And then, to test the implemented methods:

{% highlight elixir %}
iex> require Find
iex> array = [{:fruit, "Apple"}, {:vegetable, "Carrot"}, {:fruit, "Orange"}]
iex> Find.first_match(array)
{:fruit, "Apple"}
iex> Find.all_matches(array)
[{:fruit, "Apple"}, {:fruit, "Orange"}]
iex> map = %{fruit: "Apple", vegetable: "Carrot"}
iex> Find.first_match(map)
{:fruit, "Apple"}
iex> Find.all_matches(map)
[{:fruit, "Apple"}]
{% endhighlight %}

**Additional reading:**

- [Enum](http://elixir-lang.org/docs/stable/elixir/Enum.html)
- [Pattern Matching](http://elixir-lang.org/getting-started/pattern-matching.html)
