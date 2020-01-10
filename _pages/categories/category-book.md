---
title: "Post about Book"
layout: archive
permalink: /categories/book
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.book | sort:"date" %}

{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
