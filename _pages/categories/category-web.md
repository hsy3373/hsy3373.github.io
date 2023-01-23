---
title: "WEB"
layout: archive-test
permalink: categories/WEB
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.HTML %}
{% if site.categories.CSS %}
{% assign posts2 = site.categories.CSS  %}
{% for post in posts2 %} {% include archive-single4.html type=page.entries_layout %} {% endfor %}
{% endif %}
{% for post in posts %} {% include archive-single4.html type=page.entries_layout %} {% endfor %}
