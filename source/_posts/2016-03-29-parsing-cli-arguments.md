---
layout: post
title:  "Parsing command line arguments"
keywords: "cli, argument parsing, command line"
category: "cli"
comments: true
---

Use [`OptionParser.parse`](http://elixir-lang.org/docs/stable/elixir/OptionParser.html) to parse user-supplied command line arguments into a keyword list:


{% highlight elixir %}

iex> OptionParser.parse(["--source-path", "lib", "test/enum_test.exs", "--verbose"])
{[source_path: "lib", verbose: true], ["test/enum_test.exs"], []}

{% endhighlight %}

The return value is a triple (a 3-size tuple) containing three lists:

- a keyword list of flags/switches and their values
- a list of other non-switch arguments
- a keyword list of invalid flags and their values

You can pattern match the resulting tuple:

{% highlight elixir %}

parsed = OptionParser.parse(["--source-path", "lib", "test/enum_test.exs", "--verbose"])
case parsed do
	{[verbose: true], [filepath], _} -> :do_verbose_thing
	{_, [filepath], _} -> :do_thing
	_ -> :help
end

{% endhighlight %}

Supply the `strict` parameter for enforcing allowed flags:

{% highlight elixir %}
iex> OptionParser.parse(["--source-path", "lib", "test/enum_test.exs", "--verbose"], 
			strict: [source_path: :string])
{[source_path: "lib"], ["test/enum_test.exs"], [{"--verbose", nil}]}

{% endhighlight %}

Invalid flags such as `verbose` in the above example are returned in the third list of the `OptionParser.parse` result.

> Elixir converts flags/switches to underscore atoms, so --source-path becomes :source_path, to better suit Elixir conventions. This means that option names on the command line cannot contain underscores; such options will be put in the invalid options list.

`strict` can also enforce argument types:

{% highlight elixir %}
iex> OptionParser.parse(["--limit", "xyz"], strict: [limit: :integer])
{[], [], [{"--limit", "xyz"}]}
{% endhighlight %}

The above `limit` flag failed because we expected `integer`, but received `string` instead.

**Additional reading:**

- [OptionParser](http://elixir-lang.org/docs/stable/elixir/OptionParser.html)
- `iex> h OptionParser.parse`