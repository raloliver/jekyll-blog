---
layout: default
---
<div class="content list">
  {% if site.data.posts == 0 %}
    <h2>No post found</h2>
  {% else %}           
    {% for post in site.data.posts %}
    <div class="list-item">
        <h2 class="list-post-title">
          <a href="{{ post.url }}">{{ post.title }}</a>
        </h2>
        <div class="list-post-date">        
          <time>{{ post.date | date_to_string }} | {{post.tags | sort | join: ", "}}</time>
        </div>
    </div>
    {% endfor %}
    {% for post in site.posts %}
      <div class="list-item">
        <h2 class="list-post-title">
          <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
        </h2>
        <div class="list-post-date">
          <time>{{ post.date | date_to_string }} | {{post.tags | sort | join: ", "}}</time>
        </div>
      </div>
    {% endfor %} 
  {% endif %}
</div>