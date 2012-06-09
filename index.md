---
layout: default
title: 老王博客
---
<div class="row">
  <div class="span12">
    <div class="hero-unit">
      <h1>老王很忙，尚未开张</h1>
      <p>愤怒中年、技术控，外加各种不靠谱老宅男一枚。</p>
      <p><a class="btn btn-primary btn-large" href="{{ site.archive_path }}">所有文章</a></p>
    </div>
  </div>
  <div class="span4 offset4">
  <p>
  {% for post in site.posts %}
  <a class="btn btn-info" href="{{ post.url }}">[临时连接，童鞋们点这里] {{ post.title }} &rarr;</a>
  {% endfor %}
  </p>
  </div>
</div>
