---
layout: post
title:  "Documentation with ExDoc"
keywords: "documentation"
category: "documentation"
comments: true
---

To generate documentation from `@doc` and `@moduledoc` attributes in your source code, add `ex_doc` and a markdown processor as dependencies into your `mix.exs` file: 

{% highlight elixir %}
# config/mix.exs

def deps do
  [{:ex_doc, "~> 0.11", only: :dev}]
end
{% endhighlight %}

> You can use Markdown within Elixir `@doc` and `@moduledoc` attributes.

Then, run `mix deps.get` to fetch and compile the new modules and generate the project documentation with `mix docs`. 
An example output is the [official Elixir Docs](http://elixir-lang.org/docs/stable/elixir/).



**Additional reading:**

- [ex_doc](https://github.com/elixir-lang/ex_doc)
