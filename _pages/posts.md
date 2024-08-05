---
permalink: /posts
layout: default
title: All posts
---

{% for post in site.posts %}
| [**{{ post.title }}**]({{ post.url }})<br>{{ post.date | date: "%A, %B %d, %Y" }}<br>{{ post.category }} |
{% endfor %}
