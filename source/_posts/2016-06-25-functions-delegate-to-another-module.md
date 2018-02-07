---
layout: post
title:  "Functions that delegate to another module"
keywords: "nodes, connect"
category: "modules"
comments: true
---

Use `defdelegate` to define functions that delegate to functions of the same name defined in another module:

{% highlight elixir %}
defmodule Math do
  defdelegate pi, to: :math
end
{% endhighlight %}

{% highlight elixir %}
iex> Math.pi
3.141592653589793
{% endhighlight %}

Another example - protocols with default implementation:

{% highlight elixir %}
defmodule ReversableString do
    # ...

    def reverse(s) do
        # Implementation omitted
    end

    # ...
end
{% endhighlight %}

{% highlight elixir %}
defimpl Reversable, for: ReversableString do
  defdelegate reverse(self), to: ReversableString
end
{% endhighlight %}


[Read more](http://elixir-lang.org/docs/stable/elixir/Kernel.html#defdelegate/2).
