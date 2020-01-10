---
title: "Post about CI/CD"
layout: archive
permalink: /categories/cicd
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.CICD | sort:"date" %}

{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
