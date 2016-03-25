---
layout: post
title:  "Regular expressions"
keywords: "regex, regular expressions"
category: "strings"
comments: true
---

The `Regex` module gives us the following methods:

- `run`
- `scan`
- `split`
- `replace`

> Elixir's regex is based on [PCRE](http://www.pcre.org) (Perl Compatible Regular Expressions). 

`run` runs the regular expression against the given string until the first match.

{% highlight elixir %}
iex> Regex.run(~r{c(d)}, "abcd")
["cd", "d"]
iex> Regex.run(~r{e}, "abcd")
nil
{% endhighlight %}

> You can use the `~r{<regex>}` sigil or `~r/<regex>/`. Using the curly brackets version is more convenient as you can match `/` forward slash characters without having to escape it.

`scan` performs `run` several times collecting all matches of the regular expression. 

{% highlight elixir %}
iex> Regex.scan(~r/c(d|e)/, "abcd abce")
[["cd", "d"], ["ce", "e"]]
{% endhighlight %}

`split` splits the given target based on the given pattern.

{% highlight elixir %}
iex> Regex.split(~r/-/, "a-b-c")
["a", "b", "c"]
{% endhighlight %}

`replace` takes in a regex, a string and a replacement, returns a new string where all matches are replaced by the replacement.

{% highlight elixir %}
iex> Regex.replace(~r/b/, "abc", "d")
"adc"

iex> Regex.replace(~r/b/, "abc", "[\\0]") #\\N refers to the Nth character of the match
"a[b]c"

iex> Regex.replace(~r/a(b|d)c/, "abcadc", "[\\1]")
"[b][d]"

iex> Regex.replace(~r/a(b|d)c/, "abcadc", fn _, x -> "[#{x}]" end) # You can also pass functions as the replacement argument
"[b][d]"
{% endhighlight %}

**Additional reading:**

- [Regex](http://elixir-lang.org/docs/stable/elixir/Regex.html)