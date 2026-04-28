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
  min-height: 4.5em;
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
{% comment %} 1. WebP-Liste für Dubletten-Check erstellen {% endcomment %}
{% capture webp_list %}{% for file in site.static_files %}{% if file.path contains '.webp' %}{{ file.path | remove: '.webp' }}|{% endif %}{% endfor %}{% endcapture %}

{% for file in site.static_files %}
  {% if file.path contains 'images/' %}
    {% assign ext = file.extname | downcase %}
    {% assign base = file.path | remove: file.extname %}
    
    {% if ext == '.webp' or ext == '.png' or ext == '.jpg' or ext == '.jpeg' %}
      {% if file.basename != 'observatory-logo' %}
        
        {% assign skip = false %}
        {% if ext != '.webp' %}
          {% if webp_list contains base %}
            {% assign skip = true %}
          {% endif %}
        {% endif %}

        {% unless skip %}
          <div class="gallery-item">
            <div class="img-container">
              <img src="{{ site.baseurl }}{{ file.path }}" alt="{{ file.basename }}">
            </div>
            
            <div class="img-caption">
              {% comment %} Kern-ID holen (z.B. 0053) {% endcomment %}
              {% assign filename_parts = file.basename | split: '_' %}
              {% assign article_id = filename_parts[0] %}
              {% assign id_check = article_id | append: "-" %}
              
              {% assign found_article = nil %}

              {% comment %} Suche in site.pages (kompatibler als html_pages) {% endcomment %}
              {% for p in site.pages %}
                {% if p.path contains 'analysis/' %}
                  {% comment %} Wir prüfen, ob die ID am Anfang des Dateinamens steht {% endcomment %}
                  {% if p.path contains id_check %}
                    {% assign found_article = p %}
                  {% endif %}
                {% endif %}
              {% endfor %}

              {% if found_article %}
                <a href="{{ site.baseurl }}{{ found_article.url }}" target="_blank" rel="noopener noreferrer">
                  {{ found_article.title | default: article_id | truncate: 60 }} ↗
                </a>
              {% else %}
                <span style="color: #ffaa00; font-style: italic; font-size: 0.8em;">
                  Artifact {{ article_id }} (Unlinked)
                </span>
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
