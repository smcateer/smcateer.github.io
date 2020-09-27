---
layout: default
Title: Welcome
---
Test: {{site.posts[0].title}}
<ul>

Posts:
{% for post in site.posts %}
<li>
    {{ post.date | date: "%-d %B %Y" }} - 
      <a href="{{ site.path }}{{ post.url }}">
        {{ post.title }}
      </a>
{% endfor %}

</ul>
