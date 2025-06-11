---
layout: archive
author_profile: true
custom_css: /assets/css/custom_css
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
tags: [kibana, filters, tools]
last_updated: 2025-06-10
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

.content-wrapper {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.archive {
  width: 100% !important;
  max-width: none !important;
}

.page__content {
  width: 100% !important;
  max-width: none !important;
}

.filter-section {
  background: rgba(0, 255, 213, 0.05);
  border-left: 4px solid #00ffd5;
  padding: 1.5rem;
  margin: 1.5rem 0;
  border-radius: 0 8px 8px 0;
}

.code-block {
  background: rgba(0, 0, 0, 0.6);
  border: 1px solid #333;
  border-radius: 4px;
  padding: 1rem;
  font-family: 'Fira Code', monospace;
  color: #00ffd5;
  overflow-x: auto;
}

.tip-box {
  background: rgba(255, 76, 240, 0.1);
  border: 1px solid #ff4cf0;
  border-radius: 8px;
  padding: 1rem;
  margin: 1rem 0;
}

.tip-box h4 {
  color: #ff4cf0;
  margin-top: 0;
}
/* Add bold styling */
strong, b {
  color: #00ffd5;
  font-weight: bold;
}
</style>

<div class="content-wrapper">

<div class="filter-section">

<strong style="color: #00ffd5; font-weight: bold;">Fuzzy Searches</strong><br>
Find results similar to query  
Ex: host_name:server01~1  
Will match results with one level of deviance (servor)  

</div>

## Common Filter Examples

### Basic Field Filtering

<div class="code-block">
# Filter by specific field value
status:200

# Filter by multiple values
status:(200 OR 404)

# Filter by field range
response_time:[100 TO 500]
</div>

### Date Range Filtering

<div class="code-block">
# Last 24 hours
@timestamp:[now-24h TO now]

# Specific date range
@timestamp:[2025-06-01 TO 2025-06-10]
</div>

<div class="tip-box">

#### Pro Tip
Use the time picker in Kibana's interface for quick date range selection, or create custom filters for more complex time-based queries.

</div>

### Advanced Query Techniques

<div class="filter-section">

**Wildcard Searches**: Use `*` and `?` for pattern matching
- `user.name:john*` (matches john, johnny, etc.)
- `ip:192.168.1.?` (matches any single character)

**Boolean Logic**: Combine filters with AND, OR, NOT
- `status:200 AND method:GET`
- `NOT status:404`

**Nested Field Filtering**: Access nested objects
- `user.details.department:security`

</div>

## Filter Management

### Adding Filters
1. Click "+ Add filter" in the filter bar
2. Select field, operator, and value
3. Choose to include or exclude results

### Editing Filters
- Click on any existing filter to modify
- Toggle between include/exclude modes
- Enable/disable filters temporarily

### Saving Filters
- Pin filters to keep them across searches
- Save filter combinations as saved searches
- Export filters for reuse in other dashboards

<div class="tip-box">

#### Best Practices
- Start with broad filters and narrow down progressively
- Use field autocomplete to avoid typos
- Combine time-based and content-based filters for optimal performance
- Pin frequently used filters to save time

</div>

## Performance Considerations

- **Index Patterns**: Ensure your filters match your index pattern structure
- **Field Types**: Understand field mapping (keyword vs text fields)
- **Query Caching**: Kibana caches frequent queries for better performance
- **Time Ranges**: Narrower time ranges improve query speed

---


</div>