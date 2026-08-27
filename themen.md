---
layout: page
title: Themen
permalink: /themen/
---

{% assign alle_tags = site.tags | sort %}
{% if alle_tags.size == 0 %}

Hier sammeln sich die Beiträge nach Themen, sobald die ersten geschrieben sind.

{% else %}

<p>
{% for tag in alle_tags %}
  <a href="#{{ tag[0] | slugify }}">{{ tag[0] }}</a> ({{ tag[1].size }}){% unless forloop.last %} · {% endunless %}
{% endfor %}
</p>

{% for tag in alle_tags %}
<h2 id="{{ tag[0] | slugify }}">{{ tag[0] }}</h2>
<ul>
  {% for post in tag[1] %}
  <li>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    <small>– {{ post.date | date: "%d.%m.%Y" }}</small>
  </li>
  {% endfor %}
</ul>
{% endfor %}

{% endif %}
