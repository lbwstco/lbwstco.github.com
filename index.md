---
layout: page
title: 鸡排斗士的Blog
---

##开始使用Github+jekyll写博啦

* 先去学习Markdown



><ul class="posts">
>  {% for post in site.posts %}
>    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
>  {% endfor %}
></ul>

