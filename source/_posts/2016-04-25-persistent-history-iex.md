---
layout: post
title:  "Persistent history in IEx"
keywords: "history, iex"
category: "iex"
comments: true
---

By default, user input history in `IEx` do not persist across different sessions. 

[`erlang-history`](https://github.com/ferd/erlang-history) adds history support to both the Erlang shell and `IEx`:

{% highlight bash %}
git clone git@github.com:ferd/erlang-history.git
cd erlang-history
sudo make install
{% endhighlight %}

You can now access your previous inputs using the up and down arrow keys, even across sessions.