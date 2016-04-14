---
layout: post
title:  "Protocols"
keywords: "protocols, polymorphism"
category: "protocols"
comments: true
---

**Protocols** enable polymorphism in Elixir. Define protocols with `defprotocol`:

{% highlight elixir %}
defprotocol Log do
  def log(value, opts)
end
{% endhighlight %}

Implement a protocol with `defimpl`:

{% highlight elixir %}
require Logger
# User and Post are custom structs

defimpl Log, for: User do
  def log(user, _opts) do
    Logger.info "User: #{user.name}, #{user.age}"
  end
end

defimpl Log, for: Post do
  def log(user, _opts) do
    Logger.info "Post: #{post.title}, #{post.category}"
  end
end

{% endhighlight %}

> Instead of sharing protocol implementation with maps, structs require their own protocol implementation.

With the above implementations, we can do:

{% highlight elixir %}
iex> Log.log(%User{name: "Yos", age: 23})
22:53:11.604 [info]  User: Yos, 23
iex> Log.log(%Post{title: "Protocols", category: "Protocols"})
22:53:43.604 [info]  Post: Protocols, Protocols
{% endhighlight%}

Protocols let you dispatch to any data type, so long as it implements the protocol. This includes some built-in types such as `Atom`, `BitString`, `Tuples`, and others.

**Additional reading:**

- [Protocols](elixir-lang.org/getting-started/protocols.html)