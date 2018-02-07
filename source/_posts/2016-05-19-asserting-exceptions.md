---
layout: post
title:  "Asserting exceptions"
keywords: "assert, exunit, exceptions"
category: "testing"
comments: true
---

Use `assert_raise` to test if an exception was raised. `assert_raise` takes in an `Exception` and a function to be executed. 

{% highlight elixir %}
  test "invalid block size" do
    assert_raise(MerkleTree.ArgumentError, (fn() -> MerkleTree.new ["a", "b", "c"] end))
  end
{% endhighlight %}

As you can see, you can wrap any code you want to test in an anonymous function and pass it to `assert_raise`.