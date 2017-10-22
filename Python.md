---
layout: page
title: Python
permalink: /Python/
---
Python Page

<div class="Python">
  {% for Pythons in site.Python %}
    <article class="Python">

      <h1><a href="{{ site.baseurl }}{{ Python.url }}">{{ Python.title }}</a></h1>

      <div class="entry">
        {{ Python.excerpt }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Read More</a>
    </article>
  {% endfor %}
</div>
