---
layout: default
title: Image Gallery
---

# Image Gallery

<style>
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 30px;
}
.gallery-item {
  display: flex;
  flex-direction: column;
  background: #fff;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 10px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
}
.gallery .img-container {
  width: 100%;
  aspect-ratio: 1 / 1;
  overflow: hidden;
  border-radius: 4px;
  background: #f9f9f9;
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
.img-caption {
  margin-top: 12px;
  font-size: 0.9em;
  line-height: 1.3;
}
.img-caption a {
  color: #0066cc;
  text-decoration: none;
  font-weight: 500;
}
.img-caption a:hover {
  text-decoration: underline;
}
</style>

<div class="gallery">
{% capture webp_list %}
  {% for file in site.static_files %}
    {% if file.path contains '.webp' %}{{ file.path | remove: '.webp' }}|{% endif %}
  {% endfor %}
{% endcapture %}

{% for file in site.static_files %}
  {% if file.path contains 'images/' %}
    {% assign ext = file.extname | downcase %}
    {% assign base = file.path | remove: file.extname %}
    
    {% if ext == '.webp' or ext == '.png' or ext == '.jpg' or ext == '.jpeg' %}
      {% assign skip = false %}
      {% if ext != '.webp' and webp_list contains base %}
        {% assign skip = true %}
      {% endif %}

      {% unless skip %}
        <div class="gallery-item">
          <div class="img-container">
            <img src="{{ site.baseurl }}{{ file.path }}" alt="{{ file.basename }}">
          </div>
          
          <div class="img-caption">
            {% comment %} 
              Kernnummer extrahieren: Aus '0053_2' wird '0053'
            {% endcomment %}
            {% assign filename_parts = file.basename | split: '_' %}
            {% assign article_id = filename_parts[0] %}
            
            {% assign found_article = nil %}
            {% for post in site.pages %}
              {% if post.path contains 'analysis/' %}
                {% comment %} 
                  Wir prüfen, ob der Artikel-Dateiname mit der article_id beginnt (z.B. 0053-)
                {% endcomment %}
                {% if post.basename contains article_id %}
                  {% assign found_article = post %}
                  {% break %}
                {% endif %}
              {% endif %}
            {% endfor %}

            {% if found_article %}
              <a href="{{ site.baseurl }}{{ found_article.url }}" target="_blank" rel="noopener noreferrer">
                {{ found_article.title }} ↗
              </a>
            {% else %}
              <span style="color: #888;">Artifact {{ file.basename }}</span>
            {% endif %}
          </div>
        </div>
      {% endunless %}
    {% endif %}
  {% endif %}
{% endfor %}
</div>
