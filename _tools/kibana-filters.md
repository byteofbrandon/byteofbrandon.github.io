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
/* Base Typography */
h1, h2, h3, h4 {
  color: #00ffd5 !important;
  font-family: 'Fira Code', monospace !important;
}

p {
  color: #cccccc !important;
  font-family: 'Fira Code', monospace !important;
}

/* Links */
a {
  color: #00ffd5 !important;
  text-decoration: underline !important;
}

a:hover {
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

/* Text Styling */
strong, b {
  color: #00ffd5 !important;
  font-weight: bold !important;
}

/* Code inline */
code {
  background: rgba(0, 0, 0, 0.4) !important;
  color: #00ffd5 !important;
  padding: 0.2em 0.4em !important;
  border-radius: 3px !important;
  font-family: 'Fira Code', monospace !important;
}

/* Lists */
ul, ol {
  color: #cccccc !important;
}

li {
  margin-bottom: 0.5rem;
}
</style>

<div class="content-wrapper">

## Quick Reference Filters

<div class="filter-section">

**Fuzzy Searches**  
Find results similar to your query  
Example: `host_name:server01~1`  
*Matches results with one character difference (like "servor01")*

</div>

<div class="filter-section-alt">

**Proximity Searches**  
Find keywords within a set distance of each other  
Example: `log_message:"server error"~5`  
*Matches "server" and "error" within 5 words of each other*

</div>

<div class="filter-section">

**Regular Expressions**  
Use regex patterns for complex matching  
Example: `event_type:/ERROR|WARN/`  
*Matches logs containing either "ERROR" or "WARN"*

</div>

## Date Range Examples

<div class="code-block">
# Common time ranges
@timestamp:[now-24h TO now]           # Last 24 hours
@timestamp:[now-7d TO now]            # Last 7 days
@timestamp:[now-1M TO now]            # Last month

# Specific date ranges
@timestamp:[2025-06-01 TO 2025-06-10]
@timestamp:[2025-06-01T00:00:00 TO 2025-06-01T23:59:59]

# Date format patterns
@timestamp:[yyyy-MM-dd TO yyyy-MM-dd]
@timestamp:[yyyy-MM-ddTHH:mm:ss TO yyyy-MM-ddTHH:mm:ss]
</div>

## Field Value Filtering

<div class="code-block">
# Basic field filtering
status:200
method:GET
user.name:"john.doe"

# Multiple values
status:(200 OR 404 OR 500)
method:(GET OR POST)

# Range queries
response_time:[100 TO 500]
bytes_sent:>1000

# Wildcard searches
host_name:web*
ip_address:192.168.1.*
user.name:john?
</div>

<div class="tip-box">

#### Pro Tips
- Use quotes around values with spaces: `message:"server error"`
- Combine multiple filters with AND/OR: `status:200 AND method:GET`
- Use NOT to exclude: `NOT status:404`
- Pin frequently used filters to save time

</div>

## Advanced Query Techniques

### Boolean Logic
- `status:200 AND method:GET` - Both conditions must be true
- `status:(404 OR 500)` - Either condition can be true  
- `NOT status:404` - Exclude specific values
- `status:200 OR (status:500 AND urgent:true)` - Complex combinations

### Nested Field Queries
- `user.details.department:security`
- `server.metrics.cpu_usage:>80`
- `application.logs.level:ERROR`

### Performance Optimization
- Start with time-based filters first
- Use specific field names rather than `_all`
- Combine related filters with AND
- Use index patterns that match your data structure

---

*Last updated: {{ page.last_updated }}*

</div>