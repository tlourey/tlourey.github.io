---
title: Pages
description: Do I look like a local library?
type: index
fmContentType: default
date: 2024-12-27T13:38:00
lastmod: 2025-02-27T08:48:44.076Z
categories:
    - Index
---

[home](/)

<!--- cSpell:disable --->
<!-- markdownlint-disable MD033 --->
{% assign doclist = site.pages | sort: 'title' %}
<ul>
{% for item in doclist %}
  {% if item.type == "pages" %}
    <li>
      <a href="{{ item.url }}">{{ item.title }}</a> : {{ item.description }}
      ({% for category in item.tags %}
        {%- if forloop.length > 0 -%}
        {{ category }}{% unless forloop.last %}, {% endunless -%} {% endif %}
      {%- endfor %})
    </li>
  {% endif %}
{% endfor %}
</ul>
<!-- markdownlint-enable MD033 --->
<!--- cSpell:disable --->

<!--
For some reason this page renders incorrectly when markdown processor is set to GFM.
-->