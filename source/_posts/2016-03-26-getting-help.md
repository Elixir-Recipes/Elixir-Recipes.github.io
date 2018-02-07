---
layout: post
title:  "Getting help"
keywords: "help, documentation"
category: "IEx"
comments: true
---

`IEx` or Interactive EliXir gives you the helper `h` macro which prints the documentation of a given module or function. Documentation is retrieved from `@moduledoc` or `@doc` attributes defined in the source code of the module or function.

`h` can also accept itself as an argument:

{% highlight elixir %}
iex> h h
                                    def h()

Prints the documentation for IEx.Helpers.


                                defmacro h(term)

Prints the documentation for the given module or for the given function/arity
pair.

Examples

┃ h(Enum)
┃ #=> Prints documentation for Enum

It also accepts functions in the format fun/arity and module.fun/arity, for
example:

┃ h receive/1
┃ h Enum.all?/2
┃ h Enum.all?



{% endhighlight %}
