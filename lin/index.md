---
layout: lin
title: "Blog"
---
<!--To access the list variable tags from tagcollection.html-->
{% include tagcollection.html %}
<body>


<h3> Featured Posts </h3>
<p>{{ "---" | markdownify }}</p>

<h3>Recent Posts</h3>
{% assign sorted = site.lin | reverse %}
{% for snippet in sorted limit:3 %}
<h3>
<a href="{{ snippet.url }}">
      {{ snippet.title }}
    </a>
</h3>

<!--get date from  snippet-->
{% include getSnippetDate.html %}
<!--get taglist from  snippet-->
{% include getSnippetTags.html %}


<p>	{{ snippet.content | truncatewords:50 | markdownify }} </p>
<p>{{ "---" | markdownify }}</p>
{% endfor %}



</body>