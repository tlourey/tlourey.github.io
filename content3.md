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
{% assign usedcategories = page.categories %}
{% endfor %}
{{ usedcategories }}

**OR**

{% capture my_variable2 %}
{% for page in site.pages %}
{{ page.categories}},
{% endfor %}
{% endcapture %}

Dedup:

{{ my_variable2 | uniq | join: ", " }}

**OR**

{% assign mytestcat = site.pages[page.categories] %}
{{ mytestcat | uniq }}

**OR**

{{ site.category }}

**OR**

{{ site.collections }}

**OR**

{% assign all_categories = site.pages | map: "categories" %}

{% capture my_variable %}
{% for item in all_categories %}
{{ item }},
{% endfor %}
{% endcapture %}

Dedup:

{{ my_variable | uniq }}

## New index

<!-- {% assign mycats = "Tech, NotTech, Gaming, Funnies" | split: ", " %} -->
{% assign pages = site.pages | sort: 'title' %}

<ul>
  {% for page in pages %}
    {% if page.categories == "Tech" %}
      <li>
        <a href="{{ page.url }}">{{ page.title }}</a> : {{ page.description }}
      </li>
    {% endif %}
  {% endfor %}
</ul>
