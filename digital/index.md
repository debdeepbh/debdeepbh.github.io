---
layout: default 
title: Digital Painting
description: "ENTER HERE"
---
{% for image in site.static_files %}
    {% if image.path contains 'digital/' %}
<div>

        <img src="{{ site.baseurl }}{{ image.path }}" alt="image" />

</div>
    {% endif %}
{% endfor %}
