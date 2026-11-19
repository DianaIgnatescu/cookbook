---
title: Shopping list
permalink: /shopping-list/
---
{% assign s = site.data.shopping %}
<h1>Shopping list</h1>
<p class="muted">Week of {{ s.start | date: "%-d %b" }} · covers every cooking night. Ticks are saved on this device.</p>
<button class="reset" type="button" id="reset">Clear ticks</button>

{% for a in s.aisles %}
<h2>{{ a.aisle }}{% if a.check_cupboard %} <small class="muted">(check you have)</small>{% endif %}</h2>
<ul class="shop">
{% for i in a.items %}<li><label><input type="checkbox" data-key="{{ s.week }}|{{ i.name }}"><span class="g">{{ i.g }} g</span> {{ i.name }}{% if i.approx %} <small class="muted">{{ i.approx }}</small>{% endif %}{% if i.note or i.days %} <small class="muted note">{% if i.note %}{{ i.note }}{% endif %}{% if i.note and i.days %} · {% endif %}{% if i.days %}{{ i.days | join: ", " }}{% endif %}</small>{% endif %}</label></li>
{% endfor %}</ul>
{% endfor %}

<script>
(function () {
  var boxes = document.querySelectorAll('input[data-key]');
  function get(k) { try { return localStorage.getItem('shop:' + k) === '1'; } catch (e) { return false; } }
  function set(k, v) { try { v ? localStorage.setItem('shop:' + k, '1') : localStorage.removeItem('shop:' + k); } catch (e) {} }
  boxes.forEach(function (b) {
    b.checked = get(b.dataset.key);
    b.addEventListener('change', function () { set(b.dataset.key, b.checked); });
  });
  document.getElementById('reset').addEventListener('click', function () {
    boxes.forEach(function (b) { b.checked = false; set(b.dataset.key, false); });
  });
})();
</script>
