---
layout: post
title:  "Monitoring a process"
keywords: "concurrency, processes"
category: "concurrency"
comments: true
---

Monitoring a process notifies the monitor process if the monitored process crashes. Unlike `spawn_link`, it doesn't crash the monitoring process:

{% highlight elixir %}

# Span a new process
pid = spawn(fn -> :timer.sleep(100) end)

# Monitor the process
Process.monitor(pid)

# Kill the process
Process.exit(pid, :kill)

# Flush the messages of the inbox
flush
{:DOWN, #Reference<0.0.1.82>, :process, #PID<0.89.0>, :killed}

{% endhighlight %}
