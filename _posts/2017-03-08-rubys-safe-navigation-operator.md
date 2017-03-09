---
title: Ruby's Safe Navigation Operator
layout: post
---

Today at work, I was dealing with a very basic yet intermittent problem. The *nil* problem.<br />

As Rails developers, we face this problem everyday, if I may. Checking for `nil` values before proceeding.<br />

These were the approaches that I came up with

Let's assume `self.phone` is `nil`
{% highlight ruby %}
# BAD
phone_number = self.phone.gsub(/\W/, '') if self.phone.present?

# SMELL
phone_number = self.phone.try{gsub(/\W/, '')}

# BETTER
phone_number = self.phone&.gsub(/\W/, '')
{% endhighlight %}

The last approach uses a fancy Ruby 2.3+ syntax called the *safe navigation operator*. It works similar to `try`, but why is it better than `try` then? <br />

Well, for starters - less characters. Another cool advantage of the `&.` operator is that you can chain these together instead of using
`try { ... }`

{% highlight ruby %}
# BAD
if Post.first.comments.any? && Post.comments.first.lines.any?
  @likes = Post.first.comments.first.likes.count 
end

# SMELL
@likes = Post.first.try{ comments.first }.try{ likes.count }

# BETTER
@likes = Post.first&.comments.first&.likes.count
{% endhighlight %}

Much cleaner, more readable.<br />

Nonetheless, if you are like me and dealing with legacy Ruby code (< 2.3), the `try` or `if... else` blocks are a win. 

