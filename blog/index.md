---
layout: blog
title: "Blog"
---
<!--To access the list variable tags from tagcollection.html-->
<body>


{% assign recentPostLimit = 4 %}
{% assign wordlimit = 60 %}

<h2> Featured Posts </h2>
<p>{{ "---" | markdownify }}</p>

<h2>Recent Posts ({{ recentPostLimit }})</h2>
{% assign sorted = site.blog | reverse %}
{% for snippet in sorted limit:recentPostLimit %}
<h3>
<a href="{{ snippet.url }}">
      {{ snippet.title }}
    </a>
</h3>

<!--get date from  snippet-->
{% include getSnippetDate.html %}
<!--get taglist from  snippet-->
{% include getSnippetTags.html %}


<p>	{{ snippet.content | truncatewords:wordlimit | markdownify }} </p>
<p>{{ "---" | markdownify }}</p>
{% endfor %}



</body>
