---
layout: default
title: 博客
---

<style>
  .blog-section { margin-bottom: 2.5rem; }
  .blog-section h2 {
    border-bottom: 2px solid #0366d6;
    padding-bottom: 0.3rem;
  }
  .post-list { list-style: none; padding: 0; }
  .post-list li {
    padding: 0.6rem 0;
    border-bottom: 1px solid #e1e4e8;
    display: flex;
    align-items: baseline;
    gap: 0.8rem;
  }
  .post-list .post-date {
    color: #586069;
    font-size: 0.85rem;
    min-width: 5.5rem;
    font-family: monospace;
  }
  .post-list .post-title a {
    color: #0366d6;
    text-decoration: none;
    font-weight: 500;
  }
  .post-list .post-title a:hover { text-decoration: underline; }
  .post-list .post-tags { margin-left: auto; }
  .post-list .post-tags span {
    display: inline-block;
    background: #e1e4e8;
    color: #24292e;
    padding: 0.1rem 0.4rem;
    border-radius: 3px;
    font-size: 0.75rem;
    margin-left: 0.2rem;
  }
</style>

# 博客文章

{% assign tech_posts = site.posts | where: "category", "tech" %}
{% assign notes_posts = site.posts | where: "category", "notes" %}

<div class="blog-section">
  <h2>技术博客</h2>
  {% if tech_posts.size > 0 %}
  <ul class="post-list">
    {% for post in tech_posts %}
    <li>
      <span class="post-date">{{ post.date | date: "%Y-%m-%d" }}</span>
      <span class="post-title"><a href="{{ post.url }}">{{ post.title }}</a></span>
      <span class="post-tags">
        {% for tag in post.tags %}
          <span>{{ tag }}</span>
        {% endfor %}
      </span>
    </li>
    {% endfor %}
  </ul>
  {% else %}
  <p>暂无文章。</p>
  {% endif %}
</div>

<div class="blog-section">
  <h2>学习笔记</h2>
  {% if notes_posts.size > 0 %}
  <ul class="post-list">
    {% for post in notes_posts %}
    <li>
      <span class="post-date">{{ post.date | date: "%Y-%m-%d" }}</span>
      <span class="post-title"><a href="{{ post.url }}">{{ post.title }}</a></span>
      <span class="post-tags">
        {% for tag in post.tags %}
          <span>{{ tag }}</span>
        {% endfor %}
      </span>
    </li>
    {% endfor %}
  </ul>
  {% else %}
  <p>暂无文章。</p>
  {% endif %}
</div>
