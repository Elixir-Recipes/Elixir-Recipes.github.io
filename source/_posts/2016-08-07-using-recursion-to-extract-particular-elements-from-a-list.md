---
layout: post
title: "Using recursion to extract particular elements from a list"
kewyords: "filter, collection, enumerable"
category: collections
comments: true
---

In Elixir, or Erlang or any other functionnal programming language, you can easily manipulate lists using recursion.
In particular, you can extract elements from a list and separate them from the rest of the elements, in an efficient way.
This recipe will take as an example the case in which you have a list where magnet link and other character strings are mixed together.

{% highlight elixir %}
defmodule SortItems do

  def sort(items) when is_list(items), do: sort(items, [], [])

  defp sort([], magnets, rest), do: %{magnets: magnets, rest: rest}
  defp sort([h = "magnet:?xt=urn:btih:" <> _rst | t], magnets, rest) do
    sort(t, [h] ++ magnets, rest)
  end
  defp sort([h|t], magnets, rest), do: sort(t, magnets, [h] ++ rest)
end
{% endhighlight %}

Let's examine what we have here:

After defining the module name, we declare the `sort/1` function, that takes a list as a parameter (enforced by the use of the `is_list` guard).
This is the only function that will be exported, so we declare it with `def` instead of `defp`.  
The second declaration of `sort`, whose arity is of 3, matches only if the first element, our original list of items, is empty. It shall then take the two
accumulators, `magnets` and `rest` and insert them in a map to ease the access of the fields by dot-notation, for instance :

{% highlight elixir %}
result = sort(my_items)
result.magnets
{% endhighlight %}

The third declaration might look a bit frightening. 

{% highlight elixir %}
defp sort([h = "magnet:?xt=urn:btih:" <> _rst | t], magnets, rest) do
  sort(t, [h] ++ magnets, rest)
end
{% endhighlight %}

We pattern-match over the `head` of the first parameter of the function.

{% highlight elixir %}
h = "magnet:?xt=urn:btih:" <> _rst
{% endhighlight %}

It simply means "the first element of the first parameter starts with "magnet:?xt=urn:btih:". We discard the `rest` of the list's head by prepending a `_` to it.  
If it matches, then we call the `sort/3` function with the `tail` of the list as its first parameter, and add our matching item to the `magnets`
accumulator.

If it's not the case, that is to say if the `head` of the list of items doesn't match the "magnet:?…" pattern, then we fallback to the fourth declaration,
that simply calls `sort/3` while adding the `head` element to the `rest` accumulator.

The process will end when all the memebers of `items` are sorted either in `magnets` or in `rest`.

You can try this at home will the following data:

{% highlight elixir %}
list = ["PHP Hammer",
        "magnet:?xt=urn:btih:0122af27f4e87b2b1bcc8ef25115fafa4837bddd",
        "magnet:?xt=urn:btih:62709cdb2f01272c560541f55d32e145c1c561e1",
        "Not a magnet link!",
        "magnet:?xt=urn:btih:0d00bee593576c99b59170afa668acb2b8385ff9",
        "magnet:?xt=urn:btih:f8d128aad25cf684a8510765805a8f7c287d2ce2",
        "New Programmer’s Survival Manual",
        "magnet:?xt=urn:btih:46d9ea664da3fb64260de73b43aa4da3ace5bf1a",
        "Mr. Foo x Mr. Bar"]

SortItems.sort(list)
{% endhighlight %}

*Et voilà !*
