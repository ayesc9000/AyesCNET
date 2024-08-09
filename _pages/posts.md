---
permalink: /posts
layout: default
title: All posts
---

{% for post in site.posts %}
  {% include post.html post=post %}
{% endfor %}
