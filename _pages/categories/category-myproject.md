---
title: "MyProject"
layout: archive-test
permalink: categories/MyProject
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.MyProject %}
{% for post in posts %} {% include archive-single4.html type=page.entries_layout %} {% endfor %}
