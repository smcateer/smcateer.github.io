---
layout: default
Title: Welcome
---
<ul>

</ul>

{% for post in site.posts %}
<li>
      <a href="{{ site.path }}{{ post.url }}">
        {{ post.title }}
      </a>
{% endfor %}

<hr/>

{% for post in site.posts %}
  <article class='post'>
    {% if post.img %}
      <a href="{{ post.img_src }}">
        <img src="{{ post.img }}" alt="{{ post.img_alt }}" style="float:right;width:450px;padding:5px;" />
      </a>
    {% endif %}
    <div class="post-date"><small>{{ post.date | date: "%-d %B %Y" }}</small></div>
    <h1 class='post-title'>
      <a href="{{ site.path }}{{ post.url }}">
        {{ post.title }}
      </a>
    </h1>
    {{ post.content }}
  </article>

{% if post.tags %}
<p><small>tags: <em>{{ post.tags | join: "</em> - <em>" }}</em></small></p>
{% endif %}

<hr/>
{% endfor %}
