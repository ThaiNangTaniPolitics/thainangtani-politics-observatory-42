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
.gallery .img-container {
  width: 100%;
  aspect-ratio: 1 / 1;
  overflow: hidden;
  border-radius: 6px;
  background: #eee;
}
.gallery img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  cursor: zoom-in;
  transition: transform 0.3s ease;
}
.gallery img:hover {
  transform: scale(1.05);
}
</style>

<div class="gallery">
{% comment %} 
  1. Schritt: Wir erstellen einen langen String mit allen Pfaden, die auf .webp enden.
{% endcomment %}
{% capture webp_list %}
  {% for file in site.static_files %}
    {% if file.path contains '.webp' %}{{ file.path | remove: '.webp' }}|{% endif %}
  {% endfor %}
{% endcapture %}

{% comment %} 
  2. Schritt: Wir gehen alle Dateien durch und filtern Dubletten.
{% endcomment %}
{% for file in site.static_files %}
  {% if file.path contains 'images/' %}
    {% assign ext = file.extname | downcase %}
    {% assign base = file.path | remove: file.extname %}
    
    {% assign is_image = false %}
    {% if ext == '.webp' or ext == '.png' or ext == '.jpg' or ext == '.jpeg' %}
      {% assign is_image = true %}
    {% endif %}

    {% if is_image %}
      {% assign skip = false %}
      
      {% comment %} 
        Wenn es ein PNG oder JPG ist, schauen wir nach, ob der Pfad in unserer WebP-Liste steht.
      {% endcomment %}
      {% if ext != '.webp' %}
        {% if webp_list contains base %}
          {% assign skip = true %}
        {% endif %}
      {% endif %}

      {% unless skip %}
        <div class="img-container">
          <img src="{{ site.baseurl }}{{ file.path }}" alt="{{ file.basename }}">
        </div>
      {% endunless %}
    {% endif %}
  {% endif %}
{% endfor %}
</div>
