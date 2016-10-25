---
layout: post
title:  "Checking if a string includes a substring"
keywords: "strings, comparison, includes"
category: "strings"
comments: true
---

Use the `=~` operator to check if a string on the left-hand-side includes a substring on the right-hand-side:

{% highlight elixir %}

iex> "1test2" == "test"
false
iex> "1test2" =~ "test"
true

{% endhighlight %}

One application of `=~` in Phoenix is in controller tests:

{% highlight elixir %}


defmodule RealtimeUsers.PageControllerTest do
  use RealtimeUsers.ConnCase

  test "GET /", %{conn: conn} do
    conn = get conn, "/"
    assert html_response(conn, 200) =~ "Welcome to Phoenix!"
  end
end


{% endhighlight %}
