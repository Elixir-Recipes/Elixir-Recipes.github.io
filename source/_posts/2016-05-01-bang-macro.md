---
layout: post
title:  "Bang Macro"
keywords: "macro, bang, exception"
category: "metaprogramming"
comments: true
---

In Elixir, we have a naming convention where functions with `!` suffixed at the end of its name (`run!`) will raise an [exception](http://elixir-lang.org/getting-started/try-catch-and-rescue.html) if the function encounters an error.

One example is `Enum.fetch!` It also has a same `Enum.fetch` which does not raise exception. Both functions finds the element at the given index. The difference is `Enum.fetch!` raises `OutOfBoundsError` if the given position is outside the range of the collection.

Here's a nice [macro](elixir-recipes.github.io/metaprogramming/macros/) you can use to generate `bang!` versions of your existing non-raising functions.

{% highlight elixir %}
  @doc """
  Creates bang version of given function
  """
  defmacro bang(result) do
    quote do
      case unquote(result) do
        :ok -> nil
        {:ok, value} -> value
        {:error, error} -> raise error
      end
    end
  end
{% endhighlight %}

Let's see a full example.

{% highlight elixir %}
defmodule MyModule do

  @doc """
  Creates bang version of given function
  """
  defmacro bang(result) do
    quote do
      case unquote(result) do
        :ok -> nil
        {:ok, value} -> value
        {:error, error} -> raise error
      end
    end
  end

  @spec run(atom) :: {:ok, String.t} | {:error, String.t}
  def run(command) do
    case command do
      :success -> {:ok, "Result"}
      :fail -> {:error, "Some error"}
    end
  end

  @spec run!(atom) :: nil
  def run!(command) do
    bang(run(command))
  end

end
{% endhighlight %}

In the above code, we have two functions `run` and `run!`. Notice that we using our `bang` macro to generate the bang version of `run`.

{% highlight elixir %}
iex(1)> c "my_module.ex"
[MyModule]
iex(2)> MyModule.run :success
{:ok, "Result"}
iex(3)> MyModule.run :fail
{:error, "Some error"}
iex(4)> MyModule.run! :success
"Result"
iex(5)> MyModule.run! :fail
** (RuntimeError) Some error
    my_module.ex:26: MyModule.run!/1
{% endhighlight %}