---
title: Home
description: "All the shit you don't really want"
# sidebar: toc
type: index
published: false
---

<!-- markdownlint-disable-file -->
<!-- cspell:disable -->

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

{% comment %}
Site categories: {{ siteCategories }}
{% endcomment %}

{% assign siteCategories = siteCategories | split: ", " %}
{% assign siteCategories = siteCategories | sort %}


{% for category in siteCategories %}
{{ category }}:<br>
<ul>
  {% for page in site.pages %}
    {% for pagecategory in page.categories %}
      {% if pagecategory == category %}
        <li><a href="{{ page.url }}">{{ page.title }}</a> : {{ page.description }}
          ({% for tags in page.tags %}
            {%- if forloop.length > 0 -%}{{ tags }}{% unless forloop.last %}, {% endunless -%} {% endif %}
          {%- endfor %})
        </li>
      {% endif %}
    {% endfor %}
  {% endfor %}
</ul>
{% endfor %}
