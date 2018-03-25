---
layout: page
title: Cheatsheets
permalink: /cheatsheets/
---
{% for cheatsheet in site.cheatsheets %}
  <div>
    <h4><a href="{{ cheatsheet.url }}">{{ cheatsheet.title }}</a></h4>
  </div>
{% endfor %}