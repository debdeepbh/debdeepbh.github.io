---
layout: lin
title: "All Posts"
---
<!--To access the list variable tags from tagcollection.html-->
{% include tagcollection.html %}
<body>



<!--reversed to order put the most recent post first-->
{% for snippet in site.lin reversed %}
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

<p>{{ snippet.content  | markdownify }}</p>
<!--<p>{{ snippet.content | truncatewords:100 | markdownify }}</p>-->

<p>{{ "---" | markdownify }}</p>
{% endfor %}


</body>
