---
layout: home
title: Teach Yourself Programming in 10 Years!
tagline: " - Peter Norvig"
prettify: true
---
{% include JB/setup %}

{% for post in site.posts limit:10 %}
<article class="item-box">
    <h2><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a><small class="pull-right">{{ post.date | date_to_string }}</small></h2>
    <hr>
    <p>{{ post.content }}</p>
    <div class="tool-box">
        <a href="{{ BASE_PATH }}{{ post.url}}index.html#reply">Comments</a>
        <a href="{{ BASE_PATH }}{{ post.url }}" title="{{ post.title }}">Read more...</a>
    </div>
</article>
{% endfor %}

{% if true || site.posts.size > 10 %}
<div style="text-align: center;">
    <a href="{{ BASE_PATH  }}archive.html" class="btn btn-large">View all artilces list »</a>
</div>
{% endif %}
