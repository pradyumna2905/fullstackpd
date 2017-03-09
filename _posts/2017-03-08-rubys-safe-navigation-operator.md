---
title: Ruby's Safe Navigation Operator
layout: post
---

Today, at work I was dealing with a very basic yet intermittent problem. The *nil* problem.<br />

As Rails developers, we face this problem everyday, if I may. Checking for `nil` values before proceding.<br />

These are the approaches I came up with

{% highlight ruby %}
# SMELL
@post_title = Post.first.title if Post.first

# BETTER
@post_title = Post.first.try(:title)

# GOOD
@post_title = Post.first&.title 
{% endhighlight %}

The last approach uses a fancy Ruby 2.3+ syntax called the *safe navigation operator*. Why is it better than `try`? <br />

Well, for starters - less characters. Another cool advantage of the `&.` operator is that you can chain these together instead of using
`try { ... }`

{% highlight ruby %}
# SMELL
@likes = Post.first.try{ comments.first }.try{ likes.count }

# BETTER
@likes = Post.first&.comments.first&.likes.count
{% endhighlight %}

Much cleaner, more readable.<br />

Nonetheless, if you are like me and dealing with legacy Ruby code (< 2.3), the `if... else` blocks are a win. 

