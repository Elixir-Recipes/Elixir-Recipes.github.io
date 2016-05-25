---
layout: post
title:  "Behaviours"
keywords: "behaviours, modules"
category: "modules"
comments: true
---

**Behaviours** are a list of functions specifications that another module can implement. They are similar to  interfaces in other languages.

> If you've used the `use` keyword when writing GenServers or in the Phoenix framework, you've already used behaviours.

Here's an example behaviour:

{% highlight elixir %}
defmodule Parser do
  @callback parse(String.t) :: any
  @callback extensions() :: [String.t]
end
{% endhighlight %}

And a module that implements it:

{% highlight elixir %}
defmodule JSONParser do
  @behaviour Parser

  def parse(str), do: # ... parse JSON
  def extensions, do: ["json"]
end
{% endhighlight %}

The `@behaviour` module attribute above indicates that this module is expected to define every function defined in the `Parser` module. Missing functions will result in `undefined behaviour function` compilation errors.

Modules can have multiple `@behaviour` attributes. 
