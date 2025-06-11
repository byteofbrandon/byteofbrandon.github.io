---
layout: default
author_profile: true
header:
  overlay_color: "#000"
  overlay_filter: "0.4"
  overlay_image: /assets/images/tools-banner.png
  height: 600px
  caption: >
    <div style="text-align: left; padding-left: 2rem; max-width: 600px;">
      <h1 style="margin-bottom: 0.3rem; color: #00ffd5; font-family: 'Fira Code', monospace;">Cybersecurity Tools</h1>
      <p style="margin-top: 0; color: #ccc; font-family: 'Fira Code', monospace;">Essential tools and guides for security professionals</p>
    </div>
title: "Tools"
permalink: /tools/
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

.tools-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
  margin-top: 2rem;
}

.tool-card {
  background: rgba(0, 255, 213, 0.05);
  border: 1px solid #00ffd5;
  border-radius: 8px;
  padding: 1.5rem;
  transition: all 0.3s ease;
}

.tool-card:hover {
  background: rgba(0, 255, 213, 0.1);
  transform: translateY(-2px);
}

.tool-title {
  margin-bottom: 0.5rem;
  font-size: 1.2rem;
}

.tool-description {
  color: #aaa;
  font-size: 0.9rem;
}
</style>

<div class="archive">
  <div class="tools-grid">
    <div class="tool-card">
      <h3 class="tool-title">
        <a href="{{ '/tools/kibana-filters' | relative_url }}">Kibana Filters Overview</a>
      </h3>
      <p class="tool-description">Comprehensive guide to using filters in Kibana for log analysis and data visualization.</p>
    </div>
    
    <!-- Add more tool cards here as you create more tools -->
    <!--
    <div class="tool-card">
      <h3 class="tool-title">
        <a href="{{ '/tools/your-next-tool' | relative_url }}">Your Next Tool</a>
      </h3>
      <p class="tool-description">Description of your next cybersecurity tool or guide.</p>
    </div>
    -->
  </div>
</div>