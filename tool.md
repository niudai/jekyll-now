---
layout: index
pemalink: /tool/
---
<div class="posts">
  {% for post in site.categories.tool %}
      <h1><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h1>

      <div class="entry">
        {{ post.excerpt }}
      </div>
      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Read More</a>
  {% endfor %}
</div>