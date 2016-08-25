---
layout: post
title: "Accumulating @annotations"
kewyords: "annotations, module_attributes"
category: metaprogramming
comments: true
---

Using `Module.register_attribute` and `accumulate: true` lets us collect the values of annotations in our module for later use. Observe:

{% highlight elixir %}
defmodule Greetify do

  defmacro __using__(_) do
    quote do
      Module.register_attribute __MODULE__, :greet, accumulate: true,
        persist: false
      @before_compile Greetify
    end
  end

  defmacro __before_compile__(env) do
    greetings = Module.get_attribute(env.module, :greet)
    for {name, age} <- greetings do
      IO.puts "#{name} is #{age} years old"
    end
  end

end
{% endhighlight %}

In the above example, we're collecting annotations that are named `@greet`.

We can then specify a `@before_compile` callback from the same `Greetify` module that will be called before whatever downstream module that `use` `Greetify` compiles.

> `@before_compile` provides a hook that will be invoked before the module is compiled. This makes it possible to inject functions inside the module exactly before compilation. You can think of it as an `after_*` callback in Rails.

Now let's see how this works in action:

{% highlight elixir %}

defmodule Human do
  use Greetify

  @greet {"Jon", 21}
  @greet {"Sam", 23}
end

{% endhighlight %}


When the above `Human` module is loaded, we see:

{% highlight elixir %}
iex> Jon is 21 years old
iex> Sam is 23 years old

{% endhighlight %}

Note that our `Greetify` module calls `IO.puts` to print these messages before the compilation of `Human` is complete, because of `@before_compile`.

> Note that you can pass in any Elixir term as arguments to your annotations. In the example above, we pass in a tuple.

To sum up, annotations enables you to have your library users to declaratively add or modify behaviour without modifying any actual code.
