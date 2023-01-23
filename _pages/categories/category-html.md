---
title: "HTML"
layout: archive-test
permalink: categories/HTML
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.HTML | concat : site.categories.CSS %}
{% for post in posts %} {% include archive-single4.html type=page.entries_layout %} {% endfor %}
