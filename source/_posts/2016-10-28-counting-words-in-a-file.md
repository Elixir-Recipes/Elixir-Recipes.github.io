---
layout: post
title:  "Counting words in a file"
keywords: "files, reading, counting"
category: "files"
comments: true
---

Use the `File` module to read a file.

{% highlight elixir %}

file = "foo.txt"

case File.read(file) do
  {:ok, body} ->
    body
    |> IO.puts
  {:error, reason} ->
    "Could not read file #{file} because #{reason}"
    |> IO.puts
end

{% endhighlight %}

One application of this could be to count the number of words in a file.

{% highlight elixir %}

file = "foo.txt"

case File.read(file) do
  {:ok, body} ->
    String.split(body)
    |> length
    |> IO.puts
  {:error, reason} ->
    "Could not read file #{file} because #{reason}"
    |> IO.puts
end

{% endhighlight %}
