---
title: "Post about Edu"
layout: archive
permalink: /categories/edu
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.edu | sort:"date" %}

{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
