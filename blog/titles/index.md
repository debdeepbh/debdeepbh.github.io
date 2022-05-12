---
layout: lin
title: "All Titles"
---
<small>
Total: {{ site.blog.size }}
</small>

<body>

<!--reversed to order put the most recent post first-->
{% for snippet in site.blogposts reversed %}
<h3>
    <a href="{{ snippet.url }}">
      {{ snippet.title }}
      <!--{{ snippet.tags }}-->
    </a>
</h3>

<!--get date from  snippet-->
{% include getSnippetDate.html %}
<!--get taglist from  snippet-->
{% include getSnippetTags.html %}

<!--<p>{{ snippet.content  | markdownify }}</p>-->
<!--<p>{{ snippet.content | truncatewords:100 | markdownify }}</p>-->
<p>{{ "---" | markdownify }}</p>
{% endfor %}



</body>
