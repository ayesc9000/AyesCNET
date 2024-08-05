---
permalink: /posts
layout: default
title: All posts
---

{% for post in site.posts %}
| [**{{ post.title }}**]({{ post.url }})<br>Published on {{ post.date | date: "%A, %B %d, %Y" }}<br>Posted in {{ post.category }} |
{% endfor %}
