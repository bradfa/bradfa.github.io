---
layout: page
title: Bradford Embedded
header: This is the Bradford Embedded blog
---

I'm Andrew Bradford: a developer of the embedded
<a href="http://trac.cross-lfs.org/">Cross Linux From Scratch</a> book.
I write about embedded Linux, general technology, and other assorted
random things.

## Blog Posts

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

