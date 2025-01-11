---
title: Home
description: "All the shit you don't really want"
# sidebar: toc
type: index
---

## Pages

{% assign doclist = site.pages | sort: 'title' %}
<ul>
{% for item in doclist %}
    <li><a href="{{ item.url }}">{{ item.title }}</a></li>
{% endfor %}
</ul>

## Posts

{% assign doclist = site.posts | sort: 'title' %}
<ul>
{% for item in doclist %}
    <li><a href="{{ item.url }}">{{ item.title }}</a></li>
{% endfor %}
</ul>
