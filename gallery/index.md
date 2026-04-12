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
  display: block; /* Verhindert Lücken im Grid */
}
</style>

<div class="gallery">
{% for file in site.static_files %}
  {% if file.path contains 'images/' and file.extname == '.webp' %}
    {% comment %} 
      Wir extrahieren den Basispfad ohne Endung, 
      um WebP und PNG flexibel zu verknüpfen.
    {% endcomment %}
    {% assign base_path = file.path | remove: file.extname %}
    
    <picture>
      <source srcset="{{ site.baseurl }}{{ base_path }}.webp" type="image/webp">
      <source srcset="{{ site.baseurl }}{{ base_path }}.png" type="image/png">
      <img src="{{ site.baseurl }}{{ base_path }}.png" alt="Observatory Record">
    </picture>
  {% endif %}
{% endfor %}
</div>
