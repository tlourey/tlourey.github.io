---
title: Home
description: "All the shit you don't really want"
# sidebar: toc
type: index
---

## Pages

[View all pages](https://tlourey.github.io/pages/)

{% assign doclist = site.pages | sort: 'title' %}
<ul>
{% for item in doclist %}
  {% if item.type == "pages" %}
    <li><a href="{{ item.url }}">{{ item.title }}</a></li>
  {% endif %}
{% endfor %}
</ul>

## Posts

{% assign doclist = site.posts | sort: 'title' %}
<ul>
{% for item in doclist %}
    <li><a href="{{ item.url }}">{{ item.title }}</a></li>
{% endfor %}
</ul>

## Categories

{% assign doclist = site.categories %}
<ul>
{% for item in doclist %}
  <li>{{ item.categories }}</li>
{% endfor %}
</ul>
