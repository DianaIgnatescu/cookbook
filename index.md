---
title: This week
---
{% assign week = site.data.week %}
{% assign start = week.start | date: "%-d %b" %}
<h1>Week of {{ start }}</h1>
<p class="muted">Plan {{ week.week }} · <a href="{{ '/shopping-list/' | relative_url }}">🛒 Shopping list</a></p>

<ol class="week">
{% for n in week.nights %}{% assign r = site.recipes | where: "slug", n.recipe | first %}
  <li class="night {{ n.kind }}">
    <div class="day">{{ n.day | slice: 0, 3 }}<small>{{ n.date | date: "%-d %b" }}</small></div>
    {% if r %}
    <a class="card" href="{{ r.url | relative_url }}">
      {% if n.kind == 'leftover' %}<span class="tag">Leftovers</span>{% else %}{% if n.source == 'favourite' %}<span class="tag fav">⭐ Favourite</span>{% else %}<span class="tag new">New</span>{% endif %}{% if r.portions == 2 %}<span class="tag">Makes 2</span>{% endif %}{% endif %}
      <strong>{{ r.title }}</strong>
      <span class="meta">{{ r.kcal }} kcal · <b>{{ r.protein_g }} g protein</b>{% if n.kind == 'cook' %} · {{ r.time_min }} min{% else %} · reheat{% endif %}</span>
    </a>
    {% else %}<div class="card"><strong>{{ n.recipe }}</strong></div>{% endif %}
  </li>
{% endfor %}
</ol>
