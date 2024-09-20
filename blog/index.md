---
layout: page
title: Blog
head_title: Blog
weight: 2
full_width: true
---

{%- for post in site.posts -%}
{%- assign currentyear = post.date | date: "%Y" -%}
{%- if currentyear != prevyear -%}
  {% unless forloop.first %}
</ul>
  {% endunless %}
<h2 id="{{ currentyear }}">{{ currentyear }}</h2>
<ul>
  {%- assign prevyear = currentyear -%}
{% endif %}
  <li>
    <p><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a> — <span style="font-style: italic">{{ post.date | date: '%B %-d' }}</span></p>
  </li>
{%- if forloop.last %}
</ul>
{%- endif -%}
{% else %}
<p>Watch this space for the first post!</p>
{% endfor %}