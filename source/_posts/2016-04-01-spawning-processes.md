---
layout: post
title:  "Spawning processes"
keywords: "processing, spawn, concurrency"
category: "concurrency"
comments: true
---

`spawn` creates a new Erlang VM process to run a given module, function, and arguments and returns its process id `pid`.

{% highlight elixir %}
defmodule Bob do
  def say(message) do
    IO.puts "[#{inspect self}] Bob says: #{message}"
  end
end

iex> Bob.say "I'm Bob"
[#PID<0.57.0>] Bob says: sup
:ok

iex> spawn(Bob, :say, ["I'm Bob"])
[#PID<0.101.0>] Bob says: I'm Bob
#PID<0.101.0>
{% endhighlight %}

Check the `PID`s that are printed. We've just run the `Bob.say` function as a separate process. 

**Additional reading:**

- [Processes](http://elixir-lang.org/getting-started/processes.html)
- `iex> h Process`