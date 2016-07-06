---
title: Category
layout: archive
---

{% for cat in site.categories %}
    <li>{{ cat[0] }}</li>
{% endfor %}
