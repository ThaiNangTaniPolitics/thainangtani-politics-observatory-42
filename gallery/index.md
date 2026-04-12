---
layout: default
title: Image Gallery
---

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
    <img src="{{ image.path }}" alt="">
  {% endif %}
{% endfor %}
</div>
