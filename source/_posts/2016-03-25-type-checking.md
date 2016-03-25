---
layout: post
title:  "Type Checking"
keywords: "types, static analysis, type safety"
category: typespecs
comments: true
---

While Elixir is dynamically typed, we can supply optional [`typespecs`](http://elixir-lang.org/docs/stable/elixir/typespecs.html) to make sure
our programs are [type-safe](https://en.wikipedia.org/wiki/Type_safety).
Preventing type errors ensures that there's no discrepancy between differing types of our program's constants,
variables, and functions. `Typespecs` are also useful as documentation.

Here's a simple example:

{% highlight elixir %}
defmodule Bob do
  @spec say(String.t) :: String.t
  def say(message) do
    "Bob says: #{message}"
  end
end
{% endhighlight %}

We use `@spec` to specify the type of the input and its return value in the
following format:

`@spec <method name>(<type of parameter>) :: <type of return value>`

In the example above, our method `say` takes in a `string` and returns a `string`.

> Elixir provides many [built-in types](http://elixir-lang.org/docs/stable/elixir/typespecs.html#types-and-their-syntax). You can also declare your own custom domain-specific types that can then be re-used in other modules.

What happens if the implementation doesn't match the spec? Let's modify our code:

{% highlight elixir %}
defmodule Bob do
  @spec say(String.t) :: String.t
  def say(message) do
    "Bob says: #{message}"
    123 # The return type is now integer instead of String
  end
end
{% endhighlight %}

Typespecs are not used by the compiler, so if you compile and run this code,
you'll receive no warnings and the code will run. To perform type checking,
we use [`Dialyzer`](http://erlang.org/doc/man/dialyzer.html).

> You can set up Dialyzer by installing [dialyxir](https://github.com/jeremyjh/dialyxir) globally,
and using the generated `plt` as your default `dialyzer_plt`.

Let's perform some type checking:

{% highlight bash %}
$ elixirc bob.exs # Compiles to Elixir.Bob.beam
$ dialyzer Elixir.Bob.beam
  Checking whether the PLT /Users/yosriady/.dialyzer_plt is up-to-date... yes
  Proceeding with analysis...
typespecs.exs:2: Invalid type specification for function 'Elixir.Bob':say/1. The success typing is (_) -> 123
 done in 0m1.03s
done (warnings were emitted)
{% endhighlight %}

Nice! `Dialyzer` caught our type error. We can fix it and check again:

{% highlight bash %}
$ elixirc bob.exs
$ dialyzer Elixir.Bob.beam
  Checking whether the PLT /Users/yosriady/.dialyzer_plt is up-to-date... yes
  Proceeding with analysis... done in 0m0.93s
done (passed successfully)
{% endhighlight %}

In production, we can run [dialyxir](https://github.com/jeremyjh/dialyxir) on our project directory,
which handles automatic compilation of our Elixir code. We can also set up git hooks to ensure that
all type violations are fixed prior to making/pushing commits and reap the full benefits of
static analysis.

**Additional reading:**

- [Typespecs](http://elixir-lang.org/docs/stable/elixir/typespecs.html#Notes)