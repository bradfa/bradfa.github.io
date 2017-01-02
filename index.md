---
layout: page
title: Bradford Embedded
header: This is the Bradford Embedded blog
---

I'm Andrew Bradford: an embedded software and hardware developer.  I enjoy
working on embedded Linux systems and have started creating Open Source Hardware
when I have spare time.

My Open Source Hardware projects are on the [Bradford Embedded Github page][1].

You can find me on [LinkedIn][2].  Please feel free to connect!

I also have a website which lists my [small accomplishments][3] which I started
in 2017.

[1]: https://github.com/bradfordembedded
[2]: http://www.linkedin.com/in/bradfa
[3]: http://bradfa.gitlab.io

## Blog Posts

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

