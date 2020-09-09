---
layout: default
permalink: /categories/
title: Kategorien
---

<div class="home">

{% assign sorted_categories = site.categories | sort %}

{% for category in sorted_categories %}
    {% capture category_name %}{{ category | first }}{% endcapture %}

    <h2 class="post-list-heading">{{ category_name }}</h2>

    <ul class="post-list">
      {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
      {% for post in site.categories[category_name] %}
      <li>
        {% capture url_to_use %}{{ post.url }}{% endcapture %}
        {% if post.redirect_url %}
          {% capture url_to_use %}{{ post.redirect_url }}{% endcapture %}
        {% endif %}
        {% capture title_to_use %}{{ post.title }}{% endcapture %}
        {% if post.redirect_site %}
          {% capture title_to_use %}{{ post.redirect_site | append: ": " | append: post.title }}{% endcapture %}
        {% endif %}
        <span class="post-meta">{{ post.date | date: date_format }}</span>
        <h3>
          <a class="post-link" href="{{ url_to_use | relative_url }}">
            {{ title_to_use | escape }}
          </a>
        </h3>
      </li>
      {% endfor %}
    </ul>
{% endfor %}
</div>
