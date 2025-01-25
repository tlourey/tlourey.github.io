---
title: Pages
description: Do I look like a local library?
type: index
fmContentType: default
date: 2024-12-27T13:38:00
modifieddate: 2025-01-25T04:34:08.422Z
---

[home](/)

<!--- cSpell:disable --->
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
<!--- cSpell:disable --->