---
title: Reference Pages
description: Do I look like a local library?
type: index
fmContentType: default
date: 2024-12-27T13:38:00
modifieddate: 2025-01-19T07:30:52.507Z
---

[home](/)

<!--
{% assign doclist = site.pages | sort: 'title' %}
<ol>
{% for item in doclist %}
    <li><a href="{{ item.url }}">{{ item.title }}</a></li>
{% endfor %}
</ol>
-->

{% assign doclist = site.pages | sort: 'title' %}
<ul>
{% for item in doclist %}
  {% if item.type == "pages" %}
    <li>
      <a href="{{ item.url }}">{{ item.title }}</a> : {{ item.description }}
      ({% for category in item.categories %}
        {%- if forloop.length > 0 -%}
        {{ category }}{% unless forloop.last %}, {% endunless -%} {% endif %}
      {% endfor %})
    </li>
  {% endif %}
{% endfor %}
</ul>
