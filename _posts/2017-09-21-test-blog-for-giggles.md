---
layout: default
title:  "Test blog for giggles!"
date:   2017-09-21 09:00:00 +0300
categories: jekyll update
---

You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `bundle exec jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works. Testing.

I'll just test some code:

{% highlight ex %}
def get_and_send_inbox(%Test.Player{} = state) do
  inbox = Test.GlobalInbox.Cache.get_inbox
  inbox = Enum.map(inbox, fn(i) -> i.pb_message end)
  Test.Message.dispatch state.websocket, %Pb.S2C_GlobalInbox{inbox: inbox}
  {:ok, state}
end
{% endhighlight %}
