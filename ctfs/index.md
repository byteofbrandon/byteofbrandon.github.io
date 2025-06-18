---
layout: archive
author_profile: true
header:
  overlay_color: "#000"
  overlay_filter: "0.4"
  overlay_image: /assets/images/ctf-banner.png
  height: 600px
  caption: >
    <div style="text-align: left; padding-left: 2rem; max-width: 600px;">
      <h1 style="margin-bottom: 0.3rem; color: #00ffd5; font-family: 'Fira Code', monospace;">CTF Walkthroughs</h1>
      <p style="margin-top: 0; color: #ccc; font-family: 'Fira Code', monospace;">Detailed writeups and solutions for capture the flag challenges</p>
    </div>
title: "CTFs"
permalink: /ctfs/
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

.ctf-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 1.5rem;
  margin-top: 2rem;
}

.ctf-card {
  background: rgba(0, 255, 213, 0.05);
  border: 1px solid #00ffd5;
  border-radius: 6px;
  padding: 1.5rem;
  transition: all 0.3s ease;
}

.ctf-card:hover {
  background: rgba(0, 255, 213, 0.1);
  transform: translateY(-2px);
}

.ctf-title {
  margin-bottom: 0.5rem;
  font-size: 1.2rem;
}

.ctf-description {
  color: #aaa;
  font-size: 0.9rem;
  margin-bottom: 1rem;
}

.ctf-meta {
  display: flex;
  gap: 1rem;
  font-size: 0.8rem;
  color: #888;
}

.difficulty-easy {
  color: #4caf50;
}

.difficulty-medium {
  color: #ff9800;
}

.difficulty-hard {
  color: #f44336;
}

.category-badge {
  background: rgba(0, 255, 213, 0.2);
  color: #00ffd5;
  padding: 0.2rem 0.5rem;
  border-radius: 3px;
  font-size: 0.7rem;
}
</style>

<div class="archive">
  <div class="ctf-grid">
    <!-- Network Security Challenge Card -->
    <div class="ctf-card">
      <h3 class="ctf-title">
        <a href="/ctfs/net_sec_challenge/">Network Security Challenge</a>
      </h3>
      <p class="ctf-description">Comprehensive network security CTF challenge involving packet analysis, vulnerability assessment, and network forensics.</p>
      <div class="ctf-meta">
        <span class="difficulty-medium">MEDIUM</span>
        <span class="category-badge">Network Security</span>
        <span>Networking</span>
      </div>
    </div>
    
    {% for item in site.ctfs %}
    <div class="ctf-card">
      <h3 class="ctf-title">
        <a href="{{ item.url }}">{{ item.title }}</a>
      </h3>
      <p class="ctf-description">{{ item.description | default: "CTF challenge walkthrough with detailed analysis and solution." }}</p>
      <div class="ctf-meta">
        {% if item.difficulty %}
        <span class="difficulty-{{ item.difficulty | downcase }}">
          {{ item.difficulty | upcase }}
        </span>
        {% endif %}
        {% if item.category %}
        <span class="category-badge">{{ item.category }}</span>
        {% endif %}
        {% if item.platform %}
        <span>{{ item.platform }}</span>
        {% endif %}
      </div>
    </div>
    {% endfor %}
    
    <!-- If no CTFs exist yet, show a placeholder -->
    {% if site.ctfs.size == 0 %}
    <div class="ctf-card">
      <h3 class="ctf-title">
        <a href="#" onclick="return false;" style="color: #666;">Coming Soon</a>
      </h3>
      <p class="ctf-description">Additional CTF walkthroughs will be added here as challenges are completed.</p>
      <div class="ctf-meta">
        <span class="category-badge">Various Categories</span>
      </div>
    </div>
    {% endif %}
  </div>
</div>