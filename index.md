---
layout: page
title: Post List
tagline: Supporting tagline
background: '/img/bg-index.jpg'

---
{% include JB/setup %}

<ul class="posts">
  {% for post in site.posts %}
    <li> <a href="{{ BASE_PATH }}{{ post.url }}"> <p class="font-weight-bold"> {{ post.title }}</p></a> on <span>{{ post.date | date_to_string }}</span></li>
  {% endfor %}
</ul>

