---
layout: post
title:  "Debugging"
keywords: "debugging, iex, pry"
category: "iex"
comments: true
---

Using 'IEx.pry' lets you block an operation and access its bindings. Unlike `pdb` and `pry` in Ruby, it's not a full-fledged debugger but it's a quick way to look into your execution.

{% highlight elixir %}
require IEX; # First, require the IEx module

defmodule Bob do
  def say(message) do
  	 IEX.pry # debug this line
    IO.puts "[#{inspect self}] Bob says: #{message}"
  end
end
{% endhighlight %}

Running the above code in iex will now block at the specified line. You can continue with `respawn`.

An alternative method of debugging which gives you a full fledged debugger is to use the Erlang `:debugger`.

{% highlight elixir %}
iex> c "bob.ex"
iex> :debugger.start # opens a GUI debugger
iex> :int.ni(Bob)
iex> :int.break(Bob, 4) # creates breakpoint at line 4
iex> Bob.say("Hello there")
{% endhighlight %}

![](http://i.imgur.com/csffUwm.png)

After we call our function, we can see our process with break status in the debugger. We can add a new breakpoint in the monitor window, inspect the code, see the variables and navigate it in steps.

**Additional reading:**

- [Debugger](http://erlang.org/doc/apps/debugger/debugger_chapter.html)