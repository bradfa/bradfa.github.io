---
layout: page
title: Bradford Embedded
header: This is the Bradford Embedded blog
---

I'm Andrew Bradford: a developer of the embedded
<a href="http://trac.cross-lfs.org/">Cross Linux From Scratch</a> book.
I write about embedded Linux, general technology, and other assorted
random things.

You can also find me on [Twitter][1], [LinkedIn][2], and [Google+][3].
If you want to send me email, I'm "andrew" at my domain that you're visiting
right now.

[1]: https://twitter.com/#!/BradfordEmb
[2]: http://www.linkedin.com/in/bradfa
[3]: https://plus.google.com/108506657199236487651

## Blog Posts

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

