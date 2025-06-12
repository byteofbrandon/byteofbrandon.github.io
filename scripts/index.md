---
layout: archive
author_profile: true
header:
  overlay_color: "#000"
  overlay_filter: "0.4"
  overlay_image: /assets/images/scripts-banner.png
  height: 600px
  caption: >
    <div style="text-align: left; padding-left: 2rem; max-width: 600px;">
      <h1 style="margin-bottom: 0.3rem; color: #00ffd5; font-family: 'Fira Code', monospace;">Cybersecurity Scripts</h1>
      <p style="margin-top: 0; color: #ccc; font-family: 'Fira Code', monospace;">Useful scripts for security professionals and automation</p>
    </div>
title: "Scripts"
permalink: /scripts/
---

<style>
h1, h2, h3, h4 {
  color: #00ffd5;
  font-family: 'Fira Code', monospace;
}

p {
  color: #cccccc;
  font-family: 'Fira Code', monospace;
}

a {
  color: #00ffd5;
  text-decoration: underline;
}

a:hover {
  color: #ff4cf0;
}

body {
  background-color: #0f0f0f;
}

hr {
  border-color: #00ffd5;
}

.scripts-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
  margin-top: 2rem;
}

.script-card {
  background: rgba(0, 255, 213, 0.05);
  border: 1px solid #00ffd5;
  border-radius: 8px;
  padding: 1.5rem;
  transition: all 0.3s ease;
}

.script-card:hover {
  background: rgba(0, 255, 213, 0.1);
  transform: translateY(-2px);
}

.script-title {
  margin-bottom: 0.5rem;
  font-size: 1.2rem;
}

.script-description {
  color: #aaa;
  font-size: 0.9rem;
}
</style>

<div class="archive">
  <div class="scripts-grid">
    {% for item in site.scripts %}
    <div class="script-card">
      <h3 class="script-title">
        <a href="{{ item.url }}">{{ item.title }}</a>
      </h3>
      <p class="script-description">{{ item.description | default: "Cybersecurity script for automation and analysis." }}</p>
    </div>
    {% endfor %}
    
    <!-- If no scripts exist yet, show a placeholder -->
    {% if site.scripts.size == 0 %}
    <div class="script-card">
      <h3 class="script-title">
        <a href="#" onclick="return false;" style="color: #666;">Coming Soon</a>
      </h3>
      <p class="script-description">Scripts will be added here as they become available.</p>
    </div>
    {% endif %}
  </div>
</div>