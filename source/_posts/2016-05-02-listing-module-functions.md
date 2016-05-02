---
layout: post
title:  "Listing a Module's Functions"
keywords: "module, functions"
category: "metaprogramming"
comments: true
---

Each module gets an `__info__/1` function when it's compiled. The function takes
one of the following atoms:

- `:functions`  - keyword list of public functions along with their arities
- `:macros`     - keyword list of public macros along with their arities

For example, we can list the `Kernel` module's functions:

{% highlight elixir %}
iex> Kernel.__info__ :functions
[!=: 2, !==: 2, *: 2, +: 1, +: 2, ++: 2, -: 1, -: 2, --: 2, /: 2, <: 2, <=: 2,
 ==: 2, ===: 2, =~: 2, >: 2, >=: 2, abs: 1, apply: 2, apply: 3, binary_part: 3,
 bit_size: 1, byte_size: 1, div: 2, elem: 2, exit: 1, function_exported?: 3,
 get_and_update_in: 3, get_in: 2, hd: 1, inspect: 1, inspect: 2, is_atom: 1,
 is_binary: 1, is_bitstring: 1, is_boolean: 1, is_float: 1, is_function: 1,
 is_function: 2, is_integer: 1, is_list: 1, is_map: 1, is_number: 1, is_pid: 1,
 is_port: 1, is_reference: 1, is_tuple: 1, length: 1, macro_exported?: 3,
 make_ref: 0, ...]
{% endhighlight %}