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

{% for page in site.pages %}
{% assign usedcategories = page.categories | join: ", " %}
{% endfor %}
{{ usedcategories | uniq }}

**OR**

{% for page in site.pages %}
{{ page.categories | uniq }}
{% endfor %}

**OR**

{% assign mycat = site.pages[page.categories] %}
{{ mycat | uniq }}
