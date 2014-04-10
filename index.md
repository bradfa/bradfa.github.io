---
layout: page
title: Bradford Embedded
header: This is the Bradford Embedded blog
---

I'm Andrew Bradford: an embedded software developer.  You can also find me on
[LinkedIn][2].

[2]: http://www.linkedin.com/in/bradfa

## Blog Posts

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

