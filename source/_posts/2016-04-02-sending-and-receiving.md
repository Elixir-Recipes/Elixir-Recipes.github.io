---
layout: post
title:  "Sending and Receiving"
keywords: "processes, send, receive, concurrency"
category: "concurrency"
comments: true
---

Use `send` and `receive` to communicate between processes.

{% highlight elixir %}
defmodule Person do
  def tell(receiver, message) do
    IO.puts "[#{inspect self}] Sending #{message} to #{inspect receiver}"
    send receiver, {:ok, self, message}
  end
  
  def listen do
    IO.puts "[#{inspect self}] is listening"
  	receive do
  	  {:ok, sender, message} ->
IO.puts "[#{inspect self}] Received #{message} from #{inspect sender}"
  	end
  	listen
  end
end
{% endhighlight %}

In the above module, we have two functions:

- `tell` sends a message to a receiver using `send`. `send` takes a `pid` and a message - usually a tuple
- `listen` recursively calls `receive`, which is a blocking operation that waits for a message to the current process' `pid` and executes some code in response


On `iex`:

{% highlight elixir %}
iex> jeff = spawn(Person, :listen, [])
[#PID<0.78.0>] is listening
#PID<0.78.0>
iex(3)> Person.tell(jeff, "Sup jeff")
[#PID<0.57.0>] Sending Sup jeff to #PID<0.78.0>
[#PID<0.78.0>] Received Sup jeff from #PID<0.57.0>
[#PID<0.78.0>] is listening
{:ok, #PID<0.57.0>, "Sup jeff"}

{% endhighlight %}