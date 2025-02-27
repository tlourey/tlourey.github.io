---
title: Pages
description: Do I look like a local library?
type: index
fmContentType: default
date: 2024-12-27T13:38:00
lastmod: 2025-02-27T13:46:11.709Z
---

[home](/)

<!--- cSpell:disable --->
<!-- markdownlint-disable MD033 --->
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

{% assign siteCategories = siteCategories | split: ", " %}
{% assign siteCategories = siteCategories | sort %}

{% for category in siteCategories %}
{{ category }}:<br>
<ul>
  {% for page in site.pages %}
    {% for pagecategory in page.categories %}
      {% if pagecategory == category %}
        <li><a href="{{ page.url }}">{{ page.title }}</a> : {{ page.description }}
          (Tags: {% for tags in page.tags %}
            {%- if forloop.length > 0 -%}{{ tags }}{% unless forloop.last %}, {% endunless -%} {% endif %}
          {%- endfor %})
        </li>
      {% endif %}
    {% endfor %}
  {% endfor %}
</ul>
{% endfor %}

<!-- markdownlint-enable MD033 --->
<!--- cSpell:disable --->

<!--
For some reason this page renders incorrectly when markdown processor is set to GFM. This needs to be retested after 28/02/25.
-->