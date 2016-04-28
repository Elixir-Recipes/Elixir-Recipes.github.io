---
layout: post
title:  "Writing and publishing libraries"
keywords: "library, hex"
category: "hex"
comments: true
---

Let's walk through the process of writing and publishing an `Elixir` library from start to finish. For illustrative purposes, we'll create a pretend `simple_statistics` statistics toolkit for Elixir. 

<!--more-->

> Note: if you need an actual statistics library check out [`statistics`](https://hex.pm/packages/statistics).

The full source code is available on [Github](https://github.com/Leventhan/simple_statistics).

## Create an Elixir Project

{% highlight shell %}
$ mix new simple_statistics
$ cd simple_statistics
$ mix test
{% endhighlight %}

Mix will generate the following directory structure:

{% highlight shell %}
|-- _build
|-- config/
  |-- config.exs
|-- lib/
  |-- simple_statistics.ex
|-- test/
  |-- simple_statistics_test.exs
  |-- test_helper.exs
|-- mix.exs
|-- mix.lock
|-- README.md
|-- .gitignore
{% endhighlight %}

## Write Code

You can create a new folder in `lib/` with the name of your package (`simple_statistics`) to place other modules. It's a good idea to split code to different modules for modularity. We'll create a new `lib/mean.ex` module.

{% highlight shell %}
|-- lib/
  |-- simple_statistics/
    |-- mean.ex
  |-- simple_statistics.ex
{% endhighlight %}

{% highlight elixir %}
# lib/simple_statistics/mean.ex
defmodule SimpleStatistics.Mean do
  def mean([]), do: nil
  def mean(list) do
    Enum.sum(list) / Kernel.length(list)
  end
end
{% endhighlight %}

## Write Documentation

Use `@doc` to specify docstrings. You should ideally document every major public function in your modules:

{% highlight elixir %}
# lib/simple_statistics/mean.ex
defmodule SimpleStatistics.Mean do
  @doc ~S"""
  The mean is the sum of all values over the number of values.
  """
  def mean([]), do: nil
  def mean(list) do
    Enum.sum(list) / Kernel.length(list)
  end
end
{% endhighlight %}

## Add Doctests

You can add `doctests` in your docstrings like so:

{% highlight elixir %}
# lib/simple_statistics/mean.ex
defmodule SimpleStatistics.Mean do
  @doc ~S"""
  The mean is the sum of all values over the number of values.

  ## Examples

      iex> SimpleStatistics.Mean.mean([])
      nil
      iex> SimpleStatistics.Mean.mean([1,2,3,4,5])
      3.0
      iex> SimpleStatistics.Mean.mean([1.5,-2.1,3,4.5,5])
      2.38

  """
  def mean([]), do: nil
  def mean(list) do
    Enum.sum(list) / Kernel.length(list)
  end
end
{% endhighlight %}

To run them as part of your test suite:

{% highlight elixir %}
# test/simple_statistics_test.ex
defmodule SimpleStatisticsTest do
  use ExUnit.Case
  doctest SimpleStatistics.Mean
end
{% endhighlight %}

{% highlight shell %}
$ mix test
.

Finished in 0.07 seconds (0.07s on load, 0.00s on tests)
1 test, 0 failures
{% endhighlight %}

## Add Type Annotations

We can use [Typespecs](http://elixir-recipes.github.io/types/type-checking/) to utilize static type checking for our functions:

{% highlight elixir %}
@spec mean(nonempty_list(number)) :: float()
def mean(list) do
  Enum.sum(list) / Kernel.length(list)
end
{% endhighlight %}

Typespecs helps ensure that there’s no discrepancy between differing types of our program’s constants, variables, and functions.

You can then perform static analysis by using `dialyzer`. First, update your `mix.exs` to add [dialyxir](https://github.com/jeremyjh/dialyxir) as a dependency:

{% highlight elixir %}
defp deps do
  [{:ex_doc, "~> 0.11", only: :dev},
   {:earmark, "~> 0.1", only: :dev},
   {:dialyxir, "~> 0.3", only: [:dev]}]
end
{% endhighlight %}

Then, run `dialyzer` - Erlang's static analysis tool:

{% highlight shell %}
$ mix dialyzer
Starting Dialyzer
dialyzer --no_check_plt --plt /Users/yosriady/.dialyxir_core_18_1.2.0.plt -Wunmatched_returns -Werror_handling -Wrace_conditions -Wunderspecs /Users/yosriady/simple_statistics/_build/dev/lib/simple_statistics/ebin
  Proceeding with analysis... done in 0m1.68s
done (passed successfully)
{% endhighlight %}

## Generate Documentation

Update your `mix.exs` to add the following dependencies:

{% highlight elixir %}
defp deps do
  [{:ex_doc, "~> 0.11", only: :dev},
   {:earmark, "~> 0.1", only: :dev}]
end
{% endhighlight %}

Then, run:

{% highlight shell %}
$ mix docs
$ cd docs
$ open index.html
{% endhighlight %}

![](http://i.imgur.com/YkPzIyI.png)

> Here is the [live documentation](http://yosriady.com/simple_statistics), hosted on Github Pages.

As you can see, our documentation also displays docstring examples as well as any type annotations. Cool!

## Publishing your Library

We're now ready to start publishing our library.

### Register with Hex

First, you need to set up an account on [Hex](http://hex.pm), Erlang and Elixir's package manager:

{% highlight shell %}
$ mix hex.user register
{% endhighlight %}

Click on the email confirmation link to activate your Hex.pm acccount.

### Set your project's metadata

Update your `mix.exs`:

{% highlight elixir %}
# mix.exs
def project do
  [app: :decision_tree,
   version: "0.0.1",
   elixir: "~> 1.2",
   build_embedded: Mix.env == :prod,
   start_permanent: Mix.env == :prod,
   description: description,
   package: package,
   deps: deps]
end

defp description do
  """
  A few sentences (a paragraph) describing the project.
  """
end

defp package do
  [
   files: ["lib", "mix.exs", "README.md"],
   maintainers: ["Yos Riady"],
   licenses: ["Apache 2.0"],
   links: %{"GitHub" => "https://github.com/Leventhan/simple_statistics",
            "Docs" => "http://hexdocs.pm/simple_statistics/"}
   ]
end
{% endhighlight %}

After the package metadata and dependencies have been added to` mix.exs`, we are ready to publish the package with the [`mix hex.publish`](https://hex.pm/docs/tasks#hex_publish) command:

{% highlight shell %}
$ mix hex.publish
Publishing simple_statistics 0.0.1
  Dependencies:
  Files:
    lib/simple_statistics.ex
    lib/simple_statistics/mean.ex
    mix.exs
    README.md
  App: simple_statistics
  Name: simple_statistics
  Description: Statistics toolkit for Elixir.
  Version: 0.0.1
  Build tools: mix
  Licenses: Apache 2.0
  Maintainers: Yos Riady
  Links:
    Docs: http://hexdocs.pm/simple_statistics/
    GitHub: https://github.com/Leventhan/simple_statistics
  Elixir: ~> 1.2
  WARNING! Excluded dependencies (not part of the Hex package):
    ex_doc
    earmark
    dialyxir
Before publishing, please read Hex Code of Conduct: https://hex.pm/docs/codeofconduct
[#########################] 100%
Published at https://hex.pm/packages/simple_statistics/0.0.1
Don't forget to upload your documentation with `mix hex.docs`
{% endhighlight %}

Note that this will be published as the version specified in `mix.exs`.

> A published version can be amended or reverted with `--revert` up to one hour after its publication. If you want to revert a publication that is more than one hour old you need to contact an administrator.

## Publishing Documentation

You can publish your documentation to [Hex Docs](https://hexdocs.pm/). The documentation will be generated by running the `mix docs` task.

{% highlight shell %}
$ mix hex.docs
Docs successfully generated.
View them at "doc/index.html".
[#########################] 100%
Published docs for simple_statistics 0.0.1
Hosted at https://hexdocs.pm/simple_statistics/0.0.1
{% endhighlight %}

See the [live documentation](https://hexdocs.pm/simple_statistics).

This documentation will be accessible at `https://hexdocs.pm/my_package/1.0.0`. In addition, `https://hexdocs.pm/my_package` will always redirect to the latest published version. Instead of Hex.pm, you can alternatively host the documentation at `docs/` yourself or on Github Pages.

## Appendix: Versioning

Publish a new version by updating the `version` value in `mix.exs` and running `mix hex.publish`. 

Remember to use [Git tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging) to annotate version changes!

{% highlight shell %}
$ git tag -a v0.0.1 -m "Version 0.0.1"
$ git push origin v0.0.1 
{% endhighlight %}


## In Closing

We've succesfully written and published an Elixir library! Writing and publishing libraries in Elixir is easy and straightforward. Other developers can now add your library into their `deps` and start using it in their projects. 

Thanks for reading! Let me know if you have any feedback in the comments below.

## Additional Reading

- [Hex.pm](https://hex.pm/)
- [Publishing to Hex](https://hex.pm/docs/publish)
- [Hex Mix tasks](https://hex.pm/docs/tasks)
