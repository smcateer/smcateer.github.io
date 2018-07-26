---
layout: default
Title: Welcome
---

{% for post in site.posts %}

<article class='post'>
  <div class="post-date"><small>{{ post.date | date: "%-d %B %Y" }}</small></div>
  <h1 class='post-title'>
    <a href="{{ site.path }}{{ post.url }}">
      {{ post.title }}
    </a>
  </h1>
  {{ post.content }}
</article>

{% endfor %}
