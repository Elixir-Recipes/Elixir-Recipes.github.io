---
layout: post
title:  "How to connect and debug Elixir or Phoenix App at Heroku?"
keywords: "nodes, network, connect, heroku"
category: debug
comments: true
---

Heroku has a great feature called `heroku ps:exec` which allows you to connect to running nodes. You can use this command to connect your elixir nodes easily. And debug your nodes like in your network.

### Step 1
Let's start with `Procfile`
To run a named app at heroku your procfile should specify the app name like:
```
web: MIX_ENV=prod elixir --sname coolelixirapp -S mix run --no-halt
```

If you are using Phoenix framework:
```
web: MIX_ENV=prod elixir --sname coolelixirapp -S mix phx.server
```

### Step 2

Deploy your app with one of these Procfiles depending on your app type.

### Step 3

On your local:

```bash
$ heroku config # list your heroku app configs
$ heroku ps:exec # --dyno=web.1 # will connect you to web.1 dyno
```

Note: `heroku ps:exec` command does not export your configs to the heroku `bash` shell. So you will need to export them by yourself.

### Step 4

Now you are in Heroku `bash` shell for `web.1` dyno:
```bash
$ # You may need to export env vars which listed in previous 'heroku config' execution.
$ export DATABASE_URL=postgres://username:password@hostname:5432/dbname;
$ export DATABASE_POOL_SIZE=1;
$ # .... Do your all necessary exports
$ MIX_ENV=prod iex --sname coolelixirconsole -S mix # Run a console app
```

### Step 5

Now you are in Elixir console with app name `coolelixirconsole`:
{% highlight elixir %}
>> iex(coolelixirconsole@hostname)1> Node.ping :"coolelixirapp@hostname"
>>> :pong # We are connected to our running Elixir node from heroku ps:exec console
>> iex(coolelixirconsole@hostname)2> Node.list
>>> [:"coolelixirapp@hostname"] # As expected it is in the list
>> iex(coolelixirconsole@hostname)3> # Now you can tell what to do to your app as in your network.
{% endhighlight %}

### References
- https://devcenter.heroku.com/articles/exec
- https://hexdocs.pm/phoenix/heroku.html
- http://elixir-recipes.github.io/concurrency/connecting-nodes-different-machines/
- https://gist.github.com/mustafaturan/de39ecab9f344c91f495f0f51748f7a1 (Original)
