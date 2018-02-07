---
layout: post
title:  "Guard clauses"
keywords: "functions, guard clauses, pattern matching"
category: functions
comments: true
---

We can use pattern matching in named functions. See the `Sum.to` function below, which sums up the numbers from 1 to `n`:

{% highlight elixir%}

defmodule Sum do
  def to(1), do: 1
  def to(n), do: n + to(n-1)
end

{% endhighlight %}

Unfortunately, the above implementation of `Sum.to` will not work for negative numbers. In fact, if you try to run `Sum.to -1`, we'll be stuck in a loop. 

We want to specify additional predicates regarding the value or type of the arguments that are passed into our function. 

> For `Sum.to`, we want to make sure that `n` is a strictly nonzero positive integer.

Time to use **guard clauses**:

{% highlight elixir%}

defmodule Sum do
  def to(1), do: 1
  def to(n) when n > 0, do: n + to(n-1) # only nonzero positive numbers
end

{% endhighlight %}

We can have multiple guard clauses:

{% highlight elixir%}

defmodule Sum do
  def to(1), do: 1
  def to(n) when n > 0 and is_integer(n), do: n + to(n-1) # only nonzero positive integers
end

{% endhighlight %}

> Note that the expressions you can use as guard clauses are limited. You can't use your own functions as Elixir optimizes these clauses for performance reasons. A full list of available expressions are available [here](http://elixir-lang.org/getting-started/case-cond-and-if.html#expressions-in-guard-clauses).
