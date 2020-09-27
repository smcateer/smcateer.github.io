---
layout: default
Title: Welcome
---
Test: {{site.posts[0].title}}

<article class='page'>
  {% if site.posts[0].img %}
    <a href="{{ site.posts[0].img }}">
      <img src="{{ site.posts[0].img }}" alt="Image source: {{ site.posts[0].img }}" style="float:right;width:450px;padding:5px;" />
    </a>
  {% endif %}
  <div class="page-date"><small>{{ site.posts[0].date | date: "%-d %B %Y" }}</small></div>
  <h1 class='page-title'>
    {{ site.posts[0].title }}
  </h1>
  {{ site.posts[0].content }}
</article>

{% if page.tags %}
  <p><small>tags: <em>{{ page.tags | join: "</em> - <em>" }}</em></small></p>
{% endif %}

All posts:
<ul>
{% for post in site.posts %}
<li>
    {{ post.date | date: "%-d %B %Y" }} - 
      <a href="{{ site.path }}{{ post.url }}">
        {{ post.title }}
      </a>
{% endfor %}

</ul>
