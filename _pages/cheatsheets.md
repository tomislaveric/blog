---
layout: page
title: Cheatsheets
permalink: /cheatsheets/
---
{% for cheatsheet in site.cheatsheets %}
  <div class="cheatsheet">
    <h2><a href="{{ cheatsheet.url }}">{{ cheatsheet.title }}</a></h2>
  </div>
{% endfor %}