---
title: Pages (by Tags)
description: Do I look like a local library?
type: index
fmContentType: default
date: 2024-12-27T13:38:00
lastmod: 2025-03-07T12:42:15.986Z
published: true
isdraft: false
---

<!-- markdownlint-disable MD033 MD032 --->
\| <a href="/about">About</a> \| <a href="/">Home</a> \| <a href="/content.html">Up</a> | <a href="/pages/">Categories</a> |

<!--- cSpell:disable --->
{% for page in site.pages %}
  {% if page.tags %}
    {% for tag in page.tags %}
      {% unless siteTags contains tag %}
        {% assign siteTags = siteTags | append: tag %}
        {% if siteTags != "" %}
          {% assign siteTags = siteTags | append: ", " %}
        {% endif %}
      {% endunless %}
    {% endfor %}
  {% endif %}
{% endfor %}

{% assign siteTags = siteTags | split: ", " %}
{% assign siteTags = siteTags | sort %}

\| {% for tag in siteTags %} [{{ tag }}](#{{ tag }}) \|{%- endfor %}

{% for tag in siteTags %}
<a name="{{ tag }}">{{ tag }}</a>:<br>
<ul>
  {% for page in site.pages %}
    {% for pagetags in page.tags %}
      {% if pagetags == tag %}
        <li><a href="{{ page.url }}">{{ page.title }}</a> : {{ page.description }}
          (Categories: {% for category in page.categories %}
            {%- if forloop.length > 0 -%}<a href="https://tlourey.github.io/pages/#{{ category }}">{{ category }}</a>{% unless forloop.last %}, {% endunless -%} {% endif %}
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