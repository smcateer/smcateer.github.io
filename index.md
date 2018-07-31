---
layout: default
Title: Welcome
---
<hr/>

{% for post in site.posts %}

<article class='post'>
  <table>
    <tr>
      <td style="border-bottom-style:none">
        <div class="post-date"><small>{{ post.date | date: "%-d %B %Y" }}</small></div>
        <h1 class='post-title'>
          <a href="{{ site.path }}{{ post.url }}">
            {{ post.title }}
          </a>
        </h1>
        {{ post.content }}
      </td>
      {% if post.img %}
      <td  style="border-bottom-style:none" width="450px">
        <a href="{{ post.img_src }}">
          <img src="{{ post.img }}" alt="{{ post.img_alt }}" />
        </a>
      </td>
      {% endif %}
    </tr>
  </table>
</article>

{% if post.tags %}
  <p><small>tags: <em>{{ post.tags | join: "</em> - <em>" }}</em></small></p>
{% endif %}

<hr/>

{% endfor %}
