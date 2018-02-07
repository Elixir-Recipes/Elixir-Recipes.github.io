---
layout: post
title:  "Filtering collections"
keywords: "filter, collection, enumerable"
category: collections
comments: true
---

Elixir provides a set of functions that enumerate over collections which implement the `Enumerable` protocol. These collections include lists and maps.

`Enum.filter/2` takes two parameters:

- a collection, and
- a function which returns a `boolean`


Filtering a list:

{% highlight elixir %}
iex> numbers = [1,2,3,4]
iex> evens = Enum.filter(numbers, fn(x) -> (rem x, 2) == 0 end)
[2,4]
{% endhighlight %}

Filtering maps:

{% highlight elixir %}
iex> map = %{a: 1, b: 2}
iex> result = Enum.filter(map, fn {k, v} -> k == :a  end)
[a: 1]
{% endhighlight %}


> Note that the functions in the `Enum` module are eager. The `Stream` module allows lazy enumeration of enumerables and provides infinite streams.

A lazy filter using [streams](http://elixir-lang.org/docs/stable/elixir/Stream.html):

{% highlight elixir %}
iex> stream = 1..4
iex> evens = Stream.filter(stream, fn(x) -> (rem x, 2) == 0 end)
#Stream<[enum: 1..4, funs: [#Function<6.100286901/1 in Stream.filter/2>]]>
iex> Enum.to_list(evens)
[2,4]
{% endhighlight %}

----

**Additional reading:**

- [Enum](http://elixir-lang.org/docs/stable/elixir/Enum.html)
- [Stream](http://elixir-lang.org/docs/stable/elixir/Stream.html)
