---
title: WTF
description: And now, I'm going down to Emmett's Fix-It Shop. [cocks gun] To fix...Emmett.
---

# Why Hello There

{% assign doclist = site.pages | sort: 'title' %}
<ol>
{% for item in doclist %}
    <li><a href="{{ item.url }}">{{ item.title }}</a></li>
{% endfor %}
</ol>