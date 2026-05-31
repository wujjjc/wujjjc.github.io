---
layout: default
title: 标签
---

<style>
  .tags-cloud {
    margin: 1.5rem 0 2.5rem;
  }
  .tags-cloud a {
    display: inline-block;
    background: #e1e4e8;
    color: #24292e;
    padding: 0.3rem 0.7rem;
    border-radius: 4px;
    margin: 0.3rem 0.3rem;
    text-decoration: none;
    font-size: 0.95rem;
    transition: background 0.2s;
  }
  .tags-cloud a:hover {
    background: #0366d6;
    color: #fff;
  }
  .tag-section { margin-bottom: 2rem; }
  .tag-section h3 {
    margin-bottom: 0.5rem;
    color: #0366d6;
  }
  .tag-posts { list-style: none; padding: 0; }
  .tag-posts li {
    padding: 0.3rem 0;
  }
  .tag-posts .post-date {
    color: #586069;
    font-size: 0.85rem;
    font-family: monospace;
    margin-right: 0.8rem;
  }
  .tag-posts a {
    color: #0366d6;
    text-decoration: none;
  }
  .tag-posts a:hover { text-decoration: underline; }
</style>

# 标签

{% assign all_tags = "" | split: "" %}
{% for post in site.posts %}
  {% for tag in post.tags %}
    {% unless all_tags contains tag %}
      {% assign all_tags = all_tags | push: tag %}
    {% endunless %}
  {% endfor %}
{% endfor %}

<div class="tags-cloud">
  {% for tag in all_tags %}
    <a href="#{{ tag }}">{{ tag }}</a>
  {% endfor %}
</div>

{% for tag in all_tags %}
<div class="tag-section" id="{{ tag }}">
  <h3>{{ tag }}</h3>
  <ul class="tag-posts">
    {% for post in site.posts %}
      {% if post.tags contains tag %}
      <li>
        <span class="post-date">{{ post.date | date: "%Y-%m-%d" }}</span>
        <a href="{{ post.url }}">{{ post.title }}</a>
      </li>
      {% endif %}
    {% endfor %}
  </ul>
</div>
{% endfor %}
