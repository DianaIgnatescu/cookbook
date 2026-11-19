---
title: Cookbook
permalink: /cookbook/
---
{% assign saved = site.recipes | where: "saved", true | sort: "title" %}
<h1>Cookbook</h1>
<p class="muted">{{ saved.size }} saved recipe{% if saved.size != 1 %}s{% endif %}. Ask in Claude to save more.</p>
<input class="filter" type="search" id="q" placeholder="Search: chicken, potato, feta…" aria-label="Search recipes">
<ul class="cards" id="list">
{% for r in saved %}<li data-text="{{ r.title | downcase | escape }} {{ r.protein_source | escape }} {% for i in r.ingredients %}{{ i.name | escape }} {% endfor %}">
  <a class="card" href="{{ r.url | relative_url }}">
    <span class="tag">{{ r.protein_source | capitalize }}</span>
    <strong>{{ r.title }}</strong>
    <span class="meta">{{ r.kcal }} kcal · <b>{{ r.protein_g }} g protein</b> · {{ r.time_min }} min{% if r.portions == 2 %} · makes 2{% endif %}</span>
  </a></li>
{% endfor %}</ul>
{% if saved.size == 0 %}<p>No saved recipes yet. Reply "keep" to a recipe in your weekly plan and it'll appear here.</p>{% endif %}
<script>
document.getElementById('q').addEventListener('input', function (e) {
  var q = e.target.value.toLowerCase().trim();
  document.querySelectorAll('#list li').forEach(function (li) {
    li.hidden = q && li.dataset.text.indexOf(q) === -1;
  });
});
</script>
