---
permalink: /
layout: default
title: Home
---

I'm a college student working professionally in computer repair and IT. I have a
strong passion for basically anything related to technology and like to spend my
free time working on software and hardware projects.

I spend most of my time lurking online on sites like Slashdot, but I occasionally
write a post about something I am working on or my opinions on technology news and
other developments.

{% for post in site.tags['resume'] limit:1 %}
If you are interested in hiring me, check out my latest résumé: [{{ post.title }}]({{ post.url }})
{% endfor %}

{% include latestpost.html %}
