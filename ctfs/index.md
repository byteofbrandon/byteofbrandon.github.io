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
  flex-wrap: wrap;
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

.date-badge {
  color: #888;
  font-size: 0.7rem;
}

.stats-section {
  background: rgba(0, 255, 213, 0.08);
  border: 1px solid #00ffd5;
  border-radius: 8px;
  padding: 1.5rem;
  margin-bottom: 2rem;
  text-align: center;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}

.stat-item {
  padding: 0.5rem;
}

.stat-number {
  font-size: 1.5rem;
  font-weight: bold;
  color: #00ffd5;
}

.stat-label {
  font-size: 0.8rem;
  color: #aaa;
}
</style>

<div class="archive">
  
  <!-- Statistics Section -->
  <div class="stats-section">
    <h3 style="margin-top: 0;">Challenge Statistics</h3>
    <div class="stats-grid">
      <div class="stat-item">
        <div class="stat-number">{{ site.ctfs.size }}</div>
        <div class="stat-label">Total Challenges</div>
      </div>
      <div class="stat-item">
        <div class="stat-number">{{ site.ctfs | where: "difficulty", "Easy" | size }}</div>
        <div class="stat-label">Easy</div>
      </div>
      <div class="stat-item">
        <div class="stat-number">{{ site.ctfs | where: "difficulty", "Medium" | size }}</div>
        <div class="stat-label">Medium</div>
      </div>
      <div class="stat-item">
        <div class="stat-number">{{ site.ctfs | where: "difficulty", "Hard" | size }}</div>
        <div class="stat-label">Hard</div>
      </div>
    </div>
  </div>

  <!-- CTF Cards Grid -->
  <div class="ctf-grid">
    {% assign sorted_ctfs = site.ctfs | sort: 'last_updated' | reverse %}
    {% for item in sorted_ctfs %}
    <div class="ctf-card">
      <h3 class="ctf-title">
        <a href="{{ item.url | relative_url }}">{{ item.title }}</a>
      </h3>
      <p class="ctf-description">{{ item.description | default: "CTF challenge walkthrough with detailed analysis and solution." }}</p>
      <div class="ctf-meta">
        {% if item.difficulty %}
        <span class="difficulty-{{ item.difficulty | downcase }}">
          <strong>{{ item.difficulty | upcase }}</strong>
        </span>
        {% endif %}
        {% if item.category %}
        <span class="category-badge">{{ item.category }}</span>
        {% endif %}
        {% if item.platform %}
        <span class="category-badge" style="background: rgba(255, 76, 240, 0.2); color: #ff4cf0;">{{ item.platform }}</span>
        {% endif %}
        {% if item.last_updated %}
        <span class="date-badge">Updated: {{ item.last_updated | date: "%B %d, %Y" }}</span>
        {% endif %}
      </div>
      {% if item.tags %}
      <div style="margin-top: 0.5rem;">
        {% for tag in item.tags limit:3 %}
        <span style="background: rgba(0, 0, 0, 0.3); color: #ccc; padding: 0.1rem 0.3rem; border-radius: 2px; font-size: 0.6rem; margin-right: 0.2rem;">{{ tag }}</span>
        {% endfor %}
      </div>
      {% endif %}
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