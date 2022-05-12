---
layout: lin
title: "Tags"
---


<!--To access the list variable tags from tagcollection.html-->
{% include tagcollection.html %}
<body>

<!--Moved the tags to the layout-->
<!--Tags:-->
<!--{% for tag in tags %}-->
    <!--{% if tag != "" %}-->
<!--<div class="boxed">-->
	<!--<a href="#{{ tag }}"> {{ tag }}  </a>-->
<!--</div>-->
<!--[>&nbsp;<]-->
	<!--{% endif %}-->
<!--{% endfor %}-->

{% for tag in tags %}
	<h3 id="{{ tag | slugify }}">{{ tag }}</h3>
	<ul>
	 {% for post in site.blog %}
		 {% if post.tags contains tag %}
		 <li>
		 <h3>
		 <a href="{{ post.url }}">
		 {{ post.title }}
		 <!--<small>{{ post.date | date_to_string }}</small>-->
		 </a>
		 <!--{% for tag in post.tags %}-->
			 <!--<a class="tag" href="/blog/tag/#{{ tag | slugify }}">{{ tag }}</a>-->
		 <!--{% endfor %}-->
		 </h3>
		 </li>
		 {% endif %}
	 {% endfor %}
	</ul>
{% endfor %}

</body>

