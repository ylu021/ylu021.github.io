---
layout: page
title: Archive
---

{% for cat in site.categories %}
    <li>{{ cat[0] }}</li>
{% endfor %}
