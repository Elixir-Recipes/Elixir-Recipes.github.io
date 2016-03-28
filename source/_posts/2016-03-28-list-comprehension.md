---
layout: post
title:  "List comprehension"
keywords: "lists, list comprehension, generators"
category: "lists"
comments: true
---

Comprehensions in Elixir have the following syntax:

{% highlight elixir %}
for <generator(s) or filter(s), separated by commas> [, into: <value>], do: <expression> 
{% endhighlight %}

For example:

{% highlight elixir %}

iex> for x <- [1, 2, 3], do: x * x
[1,4,9]

{% endhighlight %}

> Generators such as `x` are named local variables you can use in the `expression` argument.
> 
> Note that variable assignments such as `x` in comprehensions are local in scope, so it doesn't affect variables with the same name in the outer scope.

We can have multiple generators `x` and `y`:

{% highlight elixir %}

iex> for x <- [1, 2, 3], y <- [4,5,6], do: x * y
[4, 5, 6, 8, 10, 12, 12, 15, 18]

{% endhighlight %}

We can use filters alongside generators. When the condition in the filter evaluates to false, that particular iteration is skipped.

{% highlight elixir %}

iex> for x <- [1, 2, 3], y < 5, y <- [4,5,6], do: x * y
[4, 8, 12]

{% endhighlight %}

> Unlike guard clauses, you can call your own module's methods within filter. 

The `into` parameter takes in a collection for storing the comprehension's results:

{% highlight elixir %}

iex> for item <- [:bananas, :milk], 
	quantity <- [5, 2], 
	into: Map.new, 
	do: {item, quantity}
{bananas: 2, milk: 2}

{% endhighlight %}


We can also use pattern matching in comprehensions:


{% highlight elixir %}
iex> prices = [ bananas: 1.80, milk: 4.00 ] # keyword list
iex> cart = [
	[id: 1, name: :bananas],
	[id: 2, name: :milk],
	[id: 3, name: :bananas],
	[id: 4, name: :yoghurt]
] # list of keyword lists
iex(20)> for item <- cart, 
	{_, item_name} <- item, # generator
	(item_name in Keyword.keys prices), # filter
	{name, price} <- prices, # generator 
	item_name == name, # filter
	do: price
[1.8, 4.0, 1.8]

{% endhighlight %}

