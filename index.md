---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Home
---
## What is this?
Hi, this is a little research blog inspired by [Larry Katz's interview with Boris Grebenshchikov in the summer of 1989](http://hdl.handle.net/2047/D20428339). For more context, please check out the [Getting Started]({% post_url 2022-04-28-getting-started %}) post.

## Posts
{% for post in site.posts %}
- {{ post.date | date: "%Y-%m-%d" }}: [{{ post.title }}]({{ post.url | absolute_url }})
{% endfor %}