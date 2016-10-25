---
layout: post
title:  "List all Phoenix routes"
keywords: "phoenix, routes"
category: "phoenix"
comments: true
---

Use the `mix phoenix.routes` to list out all your routes:

{% highlight bash %}
> mix phoenix.routes
page_path  GET  /                  RealtimeUsers.PageController :index
hello_path  GET  /hello             RealtimeUsers.HelloController :index
hello_path  GET  /hello/:messenger  RealtimeUsers.HelloController :show
{% endhighlight %}
