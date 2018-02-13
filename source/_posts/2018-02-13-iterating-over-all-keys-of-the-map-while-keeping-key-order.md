---
layout: post
title:  "Iterating over all keys of the map while keeping key order"
keywords: "collections, map, iteration, keyword list"
category: "collections"
comments: true
---

Map in Elixir does not guarantee the key sorting order.
{% highlight elixir %}
# With integer as a key, the key is ordered for the first 32 keys.
iex(1)> map = %{
  1 => 1, 2 => 2, 3 => 3, 4 => 4, 5 => 5, 6 => 6, 7 => 7,
  21 => 1, 22 => 2, 23 => 3, 24 => 4, 25 => 5, 26 => 6, 27 => 7,
  11 => 1, 12 => 2, 13 => 3, 14 => 4, 15 => 5, 16 => 6, 17 => 7,
  61 => 1, 62 => 2, 63 => 3, 64 => 4, 65 => 5, 66 => 6, 67 => 7,
  51 => 1, 52 => 2, 53 => 3, 54 => 4
}

# However, if the number of key is greater than 32, they will not be ordered.
iex(2)> map2 = %{
  1 => 1, 2 => 2, 3 => 3, 4 => 4, 5 => 5, 6 => 6, 7 => 7,
  21 => 1, 22 => 2, 23 => 3, 24 => 4, 25 => 5, 26 => 6, 27 => 7,
  11 => 1, 12 => 2, 13 => 3, 14 => 4, 15 => 5, 16 => 6, 17 => 7,
  61 => 1, 62 => 2, 63 => 3, 64 => 4, 65 => 5, 66 => 6, 67 => 7,
  51 => 1, 52 => 2, 53 => 3, 54 => 4, 55 => 5, 56 => 6, 57 => 7,
  41 => 1, 42 => 2, 43 => 3, 44 => 4, 45 => 5, 46 => 6, 47 => 7
}
{% endhighlight %}

Sometime you may want to iterate through the map while keeping the key in order, this could be done by converting it to the list.

{% highlight elixir %}
iex(3)> sorted_map = Enum.to_list(map2) |> Enum.sort(fn({key1, value1}, {key2, value2}) -> key1 < key2 end)
# [{1, 1}, {2, 2}, {3, 3}, {4, 4}, {5, 5}, {6, 6}, {7, 7}, {11, 1}, {12, 2},
 {13, 3}, {14, 4}, {15, 5}, {16, 6}, {17, 7}, {21, 1}, {22, 2}, {23, 3},
 {24, 4}, {25, 5}, {26, 6}, {27, 7}, {41, 1}, {42, 2}, {43, 3}, {44, 4},
 {45, 5}, {46, 6}, {47, 7}, {51, 1}, {52, 2}, {53, 3}, {54, 4}, {55, 5},
 {56, 6}, {57, 7}, {61, 1}, {62, 2}, {63, 3}, {64, 4}, {65, 5}, {66, 6},
 {67, 7}]
{% endhighlight %}
