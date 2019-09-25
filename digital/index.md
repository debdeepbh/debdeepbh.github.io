---
layout: default 
title: Digital Painting
description: "ENTER HERE"
---
## Digital painting

{% for image in site.static_files %}
    {% if image.path contains 'digital/' %}

[\\]: It is important to have the following line at the beginning of the line

![img]( {{ image.path }} )
    {% endif %}
{% endfor %}
