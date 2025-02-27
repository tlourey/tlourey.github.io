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

{% comment %} Get all post categories
<!-- {% for post in site.posts %}
  {% for category in post.categories %}
    {% unless siteCategories contains category %}
      {% if siteCategories != "" %}
        {% assign siteCategories = siteCategories | append: ", " %}
      {% endif %}
      {% assign siteCategories = siteCategories | append: category %}
    {% endunless %}
  {% endfor %}
{% endfor %} -->
{% endcomment %}

{% comment %} Get all page categories and append to a list of site categories {% endcomment %}
{% for page in site.pages %}
  {% if page.categories %}
    {% for category in page.categories %}
      {% unless siteCategories contains category %}
        {% assign siteCategories = siteCategories | append: category %}
        {% if siteCategories != "" %}
          {% assign siteCategories = siteCategories | append: ", " %}
        {% endif %}
      {% endunless %}
    {% endfor %}
  {% endif %}
{% endfor %}

Site categories: {{ siteCategories }}

{% for category in siteCategories %}
{{ category }}:
<ul>
  {% for page in site.pages %}
    {% if page.categories == category %}
      <li>{{ page.title }}</li>
    {% endif %}
  {% endfor %}
</ul>
{% endfor %}
