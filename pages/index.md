---
title: Pages
description: Do I look like a local library?
type: index
fmContentType: default
date: 2024-12-27T13:38:00
lastmod: 2025-02-25T05:01:37.511Z
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
      ({% for tag in item.tags %}
        {%- if forloop.length > 0 -%}
        {{ tag }}{% unless forloop.last %}, {% endunless -%} {% endif %}
      {%- endfor %})
    </li>
  {% endif %}
{% endfor %}
</ul>
<!-- markdownlint-enable MD033 --->
<!--- cSpell:disable --->