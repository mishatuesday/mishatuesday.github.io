---
layout: post
title:  "CORS in a Local Sinatra Development Environment"
date:   2022-11-16 17:15:00 -0400
categories: jekyll update
---

## "We'll talk about CORS in Phase 4"

...is what my instructor said when I mentioned CORS during Stand Up. CORS stands for Cross-Origin Resource Sharing, and it's a security measure that can prevent unauthorized API access.

*It can also prevent **authorized** API access if you don't know about it.*

**TLer; DRier:** My first solution worked for GET requests, but not for POST requests. I learned the real, global way to fix this (rarely encountered) issue.

Put this in your `config.ru` file:
{% highlight ruby %}
use Rack::Cors do
    allow do
        origins '*'
        resource '*', headers: :any, methods: [:get, :post, :delete, :put, :patch, :options, :head]
    end
end
{% endhighlight %}

and this in your `Gemfile`:
`gem "rack-cors"`

You *could* read the rest of this post, but why bother? If given the choice, **I'd rather be coding**.



**TL;DR:** If you have React and Ruby/Sinatra running on different ports and your data's not showing up, try putting
`response['Access-Control-Allow-Origin'] = 'http://localhost:3000'`
in your Sinatra `get` block (and not on the last line of the block). It's the least involved solution I found. *Of course if your React app is running on a port other than 3000, make it match.*

Here's the code for one of my endpoints, with the solution in place:

{% highlight ruby %}
    get '/gigs/:id' do
        response['Access-Control-Allow-Origin'] = 'http://localhost:3000'
        user = User.find(params[:id])
        user.gigs.order(date: :ASC).to_json
    end
{% endhighlight %}
### The Background

I'm in Flatiron School's Software Engineering program. Phase 1 was all
vanilla JavaScript, which I had some experience with. Phase 2 was React, which was totally new to me.

Now I'm in Phase 3, which is nominally the Ruby phase but it's primarily
focused on ActiveRecord and Sinatra, so we can build our own API in anticipation of learning Rails, which will come in Phase 4.

I knew how to write a React app and run it locally, and I had just learned how to write and run an ActiveRecord/Sinatra API using rake. So I thought, "ok I just run my React app on port 3000 and my API on 9292 and bingo!"  ...but it was **NOT BINGO**.

My data didn't show up in the browser, and I got a message that something called CORS had prevented my app from accessing my API endpoint.

So of course I searched for the error, and found lots of complicated code, mostly based on Rails apps, that would not work for me. My instructor said that CORS becomes important when we start using Rails, and none of my cohort seemed to be having this issue.

Luckily, I came across the idea that you can set the response authorization right in the Sinatra application controller, and it worked for me. Since it took me a while to find this solution, I decided to boost the signal with this blog post. Hopefully it helps the right person at the right time.

Again, the thing I added was:

`response['Access-Control-Allow-Origin'] = 'http://localhost:3000'`

and you have to put it in every endpoint you set up. I didn't say it was
the global solution, I said it's the least complicated.  I kind of didn't want to write this required blog post, because I have a project due and **I'd rather be coding**, but if this helps even one person get their first API up and running, it's worth it.