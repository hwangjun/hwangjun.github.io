---
title: "Post about jenkins"
layout: archive
permalink: /categories/jenkins
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.jenkins | sort:"date" %}

{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
