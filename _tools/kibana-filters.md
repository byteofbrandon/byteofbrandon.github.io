---
layout: archive
author_profile: true
header:
  overlay_color: "#000"
  overlay_filter: "0.4"
  overlay_image: /assets/images/banner.png
  height: 600px
  caption: >
    <div style="text-align: left; padding-left: 2rem; max-width: 600px;">
      <h1 style="margin-bottom: 0.3rem; color: #00ffd5; font-family: 'Fira Code', monospace;">Kibana Filters Overview</h1>
      <p style="margin-top: 0; color: #ccc; font-family: 'Fira Code', monospace;">Mastering data filtering and query techniques</p>
    </div>
title: "Kibana Filters Overview"
tags: [kibana, filters, elasticsearch, tools]
last_updated: 2025-06-11
toc: true
toc_label: "Filter Guide"
toc_icon: "filter"
---

<style>
/* Base Typography - Only apply to main content */
.page__content h1, 
.page__content h2, 
.page__content h3, 
.page__content h4,
.content-wrapper h1,
.content-wrapper h2,
.content-wrapper h3,
.content-wrapper h4 {
  color: #00ffd5 !important;
  font-family: 'Fira Code', monospace !important;
}

.page__content p,
.content-wrapper p {
  color: #cccccc !important;
  font-family: 'Fira Code', monospace !important;
}

/* Links - Only in content area */
.page__content a,
.content-wrapper a {
  color: #00ffd5 !important;
  text-decoration: underline !important;
}

.page__content a:hover,
.content-wrapper a:hover {
  color: #ff4cf0 !important;
}

/* Body and Layout */
body {
  background-color: #0f0f0f !important;
}

hr {
  border-color: #00ffd5 !important;
}

/* Content Layout */
.content-wrapper {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.archive,
.page__content {
  width: 100% !important;
  max-width: none !important;
}

/* Filter Sections */
.filter-section {
  background: rgba(0, 255, 213, 0.05);
  border-left: 4px solid #00ffd5;
  padding: 1.5rem;
  margin: 1.5rem 0;
  border-radius: 0 8px 8px 0;
}

.filter-section-alt {
  background: rgba(0, 215, 255, 0.08);
  border-left: 4px solid #00d7ff;
  padding: 1.5rem;
  margin: 1.5rem 0;
  border-radius: 0 8px 8px 0;
}

/* Code Blocks */
.code-block {
  background: rgba(0, 0, 0, 0.8);
  border: 1px solid #333;
  border-radius: 6px;
  padding: 1.5rem;
  font-family: 'Fira Code', monospace;
  color: #00ffd5;
  overflow-x: auto;
  line-height: 1.6;
}

/* Tip Boxes */
.tip-box {
  background: rgba(255, 76, 240, 0.1);
  border: 1px solid #ff4cf0;
  border-radius: 8px;
  padding: 1.5rem;
  margin: 1.5rem 0;
}

.tip-box h4 {
  color: #ff4cf0 !important;
  margin-top: 0;
}

/* Text Styling - Only in content */
.page__content strong, 
.page__content b,
.content-wrapper strong,
.content-wrapper b {
  color: #00ffd5 !important;
  font-weight: bold !important;
}

/* Code inline - Only in content */
.page__content code,
.content-wrapper code {
  background: rgba(0, 0, 0, 0.4) !important;
  color: #00ffd5 !important;
  padding: 0.2em 0.4em !important;
  border-radius: 3px !important;
  font-family: 'Fira Code', monospace !important;
}

/* Lists - Only in content */
.page__content ul, 
.page__content ol,
.content-wrapper ul,
.content-wrapper ol {
  color: #cccccc !important;
}

.page__content li,
.content-wrapper li {
  margin-bottom: 0.5rem;
}
</style>

<div class="content-wrapper">

## Quick Reference Filters

<div class="filter-section">

<strong style="color: #00ffd5; font-weight: bold;">Fuzzy Searches</strong><br>
Find results similar to your query<br>
Example: <code>host_name:server01~1</code><br>
<em>Matches results with one character difference (like "servor01")</em>

</div>

<div class="filter-section-alt">

<strong style="color: #00ffd5; font-weight: bold;">Proximity Searches</strong><br>
Find keywords within a set distance of each other<br>
Example: <code>log_message:"server error"~5</code><br>
<em>Matches "server" and "error" within 5 words of each other</em>

</div>

<div class="filter-section">

<strong style="color: #00ffd5; font-weight: bold;">Regular Expressions</strong><br>
Use regex patterns for complex matching<br>
Example: <code>event_type:/ERROR|WARN/</code><br>
<em>Matches logs containing either "ERROR" or "WARN"</em>

</div>

## Date Range Examples

<div class="code-block">
<strong style="color: #00ffd5; font-weight: bold;"># Common time ranges</strong><br>
@timestamp:[now-24h TO now]&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<strong style="color: #cccccc;"># Last 24 hours</strong><br>
@timestamp:[now-7d TO now]&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<strong style="color: #cccccc;"># Last 7 days</strong><br>
@timestamp:[now-1M TO now]&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<strong style="color: #cccccc;"># Last month</strong><br>
<br>
<strong style="color: #00ffd5; font-weight: bold;"># Specific date ranges</strong><br>
@timestamp:[2025-06-01 TO 2025-06-10]<br>
@timestamp:[2025-06-01T00:00:00 TO 2025-06-01T23:59:59]<br>
<br>
<strong style="color: #00ffd5; font-weight: bold;"># Date format patterns</strong><br>
@timestamp:[yyyy-MM-dd TO yyyy-MM-dd]<br>
@timestamp:[yyyy-MM-ddTHH:mm:ss TO yyyy-MM-ddTHH:mm:ss]<br>
</div>

## Field Value Filtering

<div class="code-block">
<strong style="color: #00ffd5; font-weight: bold;"># Multiple values</strong><br>
status:(200 OR 404 OR 500)<br>
method:(GET OR POST)<br>
<br>
<strong style="color: #00ffd5; font-weight: bold;"># Range queries</strong><br>
response_time:[100 TO 500]<br>
bytes_sent:>1000<br>
<br>
<strong style="color: #00ffd5; font-weight: bold;"># Wildcard searches</strong><br>
host_name:web*<br>
ip_address:192.168.1.*<br>
user.name:john?<br>
</div>




</div>