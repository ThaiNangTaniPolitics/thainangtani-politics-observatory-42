---
layout: default
title: Image Gallery
---

<p><a href="/thainangtani-politics-observatory/">← Back to Home</a></p>

# Image Gallery

<style>
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 20px;
}
.gallery img {
  width: 100%;
  border-radius: 6px;
  cursor: zoom-in;
}
</style>

<div class="gallery">
{% for image in site.static_files %}
  {% if image.path contains 'images/' %}
    <img src="{{ site.baseurl }}{{ image.path }}" alt="">
  {% endif %}
{% endfor %}
</div>
