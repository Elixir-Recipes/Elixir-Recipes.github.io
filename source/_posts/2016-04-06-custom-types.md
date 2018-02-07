---
layout: post
title:  "Custom types"
keywords: "processes, debug, trace, sys"
category: "types"
comments: true
---

Use `@type` to define custom types. For example, we can imagine definining types in an API client:

{% highlight elixir %}

@type body           :: any
@type status_code    :: integer
@type request_method :: :get | :put | :post | :delete | :put | :patch | :head
@type header         :: { binary, binary }
@type response       :: { status_code, any, [header] }
@type payload        :: %Payload{ method: request_method, id: binary, size: integer }

{% endhighlight %}

> You can use custom types in the definition of types, such as how the above `header` type is used in `response`. 

**Additional reading:**

- [Defining a type](http://elixir-lang.org/docs/stable/elixir/typespecs.html#defining-a-type)