---
title: Past weeks
permalink: /weeks/
---
<h1>Past weeks</h1>
{% assign keys = site.data.weeks | sort | reverse %}
{% for pair in keys %}{% assign w = pair[1] %}
<h2>{{ w.week }} <small class="muted">w/c {{ w.start | date: "%-d %b %Y" }}</small></h2>
<ul class="plain">
{% for n in w.nights %}{% if n.kind == 'cook' %}{% assign r = site.recipes | where: "slug", n.recipe | first %}
<li>{{ n.day | slice: 0, 3 }}: {% if r %}<a href="{{ r.url | relative_url }}">{{ r.title }}</a>{% else %}{{ n.recipe | replace: '-', ' ' }} <small class="muted">(not saved)</small>{% endif %}</li>
{% endif %}{% endfor %}
</ul>
{% endfor %}
