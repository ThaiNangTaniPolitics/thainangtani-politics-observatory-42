---
layout: default
title: Image Gallery
---

# Image Gallery

<style>
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 25px;
  padding: 10px 0;
}
.gallery-item {
  display: flex;
  flex-direction: column;
  background: #ffffff;
  border: 1px solid #e1e4e8;
  border-radius: 8px;
  padding: 12px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.08);
  transition: all 0.2s ease-in-out;
}
.gallery-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(0,0,0,0.1);
  border-color: #0366d6;
}
.gallery .img-container {
  width: 100%;
  aspect-ratio: 1 / 1;
  overflow: hidden;
  border-radius: 4px;
  background: #f6f8fa;
}
.gallery img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  cursor: zoom-in;
}
.img-caption {
  margin-top: 12px;
  font-size: 0.82em;
  line-height: 1.4;
  min-height: 4.2em;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.img-caption a {
  color: #0366d6;
  text-decoration: none;
  font-weight: 600;
  margin-bottom: 4px;
}
.img-caption a:hover {
  text-decoration: underline;
}
.artifact-id {
  color: #6a737d;
  font-family: "SFMono-Regular", Consolas, "Liberation Mono", Menlo, monospace;
  font-size: 0.85em;
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
      {% if file.basename != 'observatory-logo' %}
        
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
                1. Extrahiere die ID (z.B. 0053) vom Bildnamen
              {% endcomment %}
              {% assign filename_parts = file.basename | split: '_' %}
              {% assign article_id = filename_parts[0] %}
              
              {% assign found_article = nil %}

              {% comment %}
                2. Suche in allen Dokumenten (nicht pages!) nach passendem Artikel
              {% endcomment %}
              {% for p in site.documents %}
                {% if p.url contains '/analysis/' %}
                  {% assign path_parts = p.path | split: '/' %}
                  {% assign real_filename = path_parts | last %}
                  
                  {% if real_filename starts_with article_id %}
                    {% assign found_article = p %}
                    {% break %}
                  {% endif %}
                {% endif %}
              {% endfor %}

              {% if found_article %}
                <a href="{{ found_article.url }}" target="_blank" rel="noopener noreferrer">
                  {{ found_article.title | default: found_article.basename | truncate: 65 }} ↗
                </a>
              {% else %}
                <span style="color: #d1d5da; font-style: italic;">Mapping: {{ article_id }}?</span>
              {% endif %}

              <span class="artifact-id">ID: {{ file.basename }}</span>
            </div>
          </div>
        {% endunless %}
      {% endif %}
    {% endif %}
  {% endif %}
{% endfor %}
</div>
