---
permalink: /posts
layout: default
title: All posts
---

{% assign publicPosts = site.posts | where_exp: "post", "post.hidden != true" %}
{% for post in publicPosts %}
  {% include post.html post=post %}
{% endfor %}
