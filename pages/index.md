---
title: Pages (by Categories)
description: Do I look like a local library?
type: index
fmContentType: default
date: 2024-12-27T13:38:00
lastmod: 2025-03-08T12:39:59.480Z
published: true
isdraft: false
---

<!-- markdownlint-disable MD033 --->
\| <a href="/about">About</a> \| <a href="/">Home</a> \| <a href="/content.html">Up</a> | <a href="/pages/tags.html">Tags</a> |

<!--- cSpell:disable --->
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

\| {% for category in siteCategories %} [{{ category }}](#{{ category }}) \|{%- endfor %}

{% for category in siteCategories %}
<a name="{{ category }}">{{ category }}:<br>
<ul>
  {% for page in site.pages %}
    {% for pagecategory in page.categories %}
      {% if pagecategory == category %}
        <li><a href="{{ page.url }}">{{ page.title }}</a> : {{ page.description }}
          (Tags: {% for tags in page.tags %}
            {%- if forloop.length > 0 -%}<a href="https://tlourey.github.io/pages/tags.html#{{ tags }}">{{ tags }}</a>{% unless forloop.last %}, {% endunless -%} {% endif %}
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