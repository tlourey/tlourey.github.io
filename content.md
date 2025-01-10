# Home

## Pages

{% assign doclist = site.pages | sort: 'title' %}
<ol>
{% for item in doclist %}
    <li><a href="{{ item.url }}">{{ item.title }}</a></li>
{% endfor %}
</ol>

## Posts

{% assign doclist = site.posts | sort: 'title' %}
<ol>
{% for item in doclist %}
    <li><a href="{{ item.url }}">{{ item.title }}</a></li>
{% endfor %}
</ol>
