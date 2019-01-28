---
layout: index
pemalink: /java/
---

<div class="posts">
  {% for post in site.categories.java %}
      <h1><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h1>
      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Read More</a>
  {% endfor %}
</div>