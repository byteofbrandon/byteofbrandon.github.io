---
layout: archive
author_profile: true
title: "Nmap Fundamentals"
description: "Complete guide to network discovery and port scanning techniques. Covers stealth scanning, service detection, and script usage."
tags: [nmap, reconnaissance, port-scanning, enumeration]
phase: "Reconnaissance"
category: "reconnaissance"
tools: ["nmap", "netdiscover", "masscan"]
difficulty: "Beginner"
last_updated: 2025-01-15
related_notes: ["service-enumeration", "stealth-scanning", "firewall-evasion"]
references: ["nmap-official-docs", "pentest-methodology"]
header:
  overlay_color: "#000"
  overlay_filter: "0.4"
  overlay_image: /assets/images/redteam-banner.png
  height: 400px
  caption: >
    <div style="text-align: left; padding-left: 2rem; max-width: 600px;">
      <h1 style="margin-bottom: 0.3rem; color: #00ffd5; font-family: 'Fira Code', monospace;">Nmap Fundamentals</h1>
      <p style="margin-top: 0; color: #ccc; font-family: 'Fira Code', monospace;">Network discovery and port scanning techniques</p>
    </div>
toc: true
toc_label: "Nmap Techniques"
toc_icon: "search"
---

<style>
/* Inherit styling from main Red Team theme */
.page__content h1, 
.page__content h2, 
.page__content h3, 
.page__content h4 {
  color: #00ffd5 !important;
  font-family: 'Fira Code', monospace !important;
  margin-top: 2rem !important;
  margin-bottom: 1rem !important;
}

.page__content p {
  color: #cccccc !important;
  font-family: 'Fira Code', monospace !important;
  line-height: 1.6 !important;
}

.page__content a {
  color: #00ffd5 !important;
  text-decoration: underline !important;
}

.page__content a:hover {
  color: #ff4cf0 !important;
}

body {
  background-color: #0f0f0f !important;
}

/* Command blocks */
.command-block {
  background: rgba(0, 0, 0, 0.8);
  border: 1px solid #333;
  border-radius: 6px;
  padding: 1.5rem;
  font-family: 'Fira Code', monospace;
  color: #00ffd5;
  overflow-x: auto;
  margin: 1rem 0;
  position: relative;
}

.command-block::before {
  content: '$ ';
  color: #ff4cf0;
  font-weight: bold;
}

/* Note sections */
.note-section {
  background: rgba(0, 255, 213, 0.05);
  border-left: 4px solid #00ffd5;
  padding: 1.5rem;
  margin: 1.5rem 0;
  border-radius: 0 8px 8px 0;
}

.warning-section {
  background: rgba(255, 193, 7, 0.08);
  border-left: 4px solid #ffc107;
  padding: 1.5rem;
  margin: 1.5rem 0;
  border-radius: 0 8px 8px 0;
}

.tip-section {
  background: rgba(76, 175, 80, 0.08);
  border-left: 4px solid #4caf50;
  padding: 1.5rem;
  margin: 1.5rem 0;
  border-radius: 0 8px 8px 0;
}

/* Inline code */
.page__content code {
  background: rgba(0, 0, 0, 0.4) !important;
  color: #00ffd5 !important;
  padding: 0.2em 0.4em !important;
  border-radius: 3px !important;
  font-family: 'Fira Code', monospace !important;
}

/* Tables */
.page__content table {
  border-collapse: collapse;
  margin: 1rem 0;
  background: rgba(0, 0, 0, 0.3);
}

.page__content th, .page__content td {
  border: 1px solid #333;
  padding: 0.8rem;
  text-align: left;
}

.page__content th {
  background: rgba(0, 255, 213, 0.1);
  color: #00ffd5;
  font-weight: bold;
}

/* Related notes */
.related-notes {
  background: rgba(255, 76, 240, 0.1);
  border: 1px solid #ff4cf0;
  border-radius: 8px;
  padding: 1.5rem;
  margin: 2rem 0;
}

.related-notes h4 {
  color: #ff4cf0 !important;
  margin-top: 0;
}

.related-notes ul {
  list-style: none;
  padding: 0;
}

.related-notes li {
  margin-bottom: 0.5rem;
  padding: 0.5rem;
  background: rgba(0, 0, 0, 0.3);
  border-radius: 4px;
}

.related-notes a {
  color: #ff4cf0 !important;
  text-decoration: none;
}

.related-notes a:hover {
  text-decoration: underline !important;
}

/* Technique boxes */
.technique-box {
  background: rgba(0, 0, 0, 0.5);
  border: 1px solid #00ffd5;
  border-radius: 8px;
  padding: 1.5rem;
  margin: 1.5rem 0;
}

.technique-box h5 {
  color: #00ffd5 !important;
  margin-top: 0;
  margin-bottom: 1rem;
}
</style>

<div class="note-section">
<h4>📍 Note Overview</h4>
<p>This guide covers the fundamentals of using Nmap for network discovery and port scanning. Nmap is essential for the reconnaissance phase of penetration testing and red team operations.</p>
</div>

## Basic Nmap Syntax

The basic syntax for Nmap follows this pattern:

<div class="command-block">
nmap [Scan Type] [Options] [Target]
</div>

### Target Specification

Nmap can target individual hosts, IP ranges, or entire subnets:

<div class="command-block">
# Single host
nmap 192.168.1.1

# Multiple hosts
nmap 192.168.1.1 192.168.1.2 192.168.1.3

# IP range
nmap 192.168.1.1-254

# Subnet
nmap 192.168.1.0/24

# From file
nmap -iL targets.txt
</div>

---

## Common Scan Types

### TCP Connect Scan (-sT)

<div class="technique-box">
<h5>🔍 TCP Connect Scan</h5>
<p>Completes the full TCP three-way handshake. More reliable but also more detectable.</p>

<div class="command-block">
nmap -sT target.com
</div>

<strong>Use Cases:</strong>
- When you don't have raw packet privileges
- More accurate results for open ports
- Default scan when run as non-root user
</div>

### SYN Scan (-sS)

<div class="technique-box">
<h5>🥷 SYN Scan (Stealth Scan)</h5>
<p>Sends SYN packets without completing the handshake. Faster and more stealthy.</p>

<div class="command-block">
nmap -sS target.com
</div>

<strong>Use Cases:</strong>
- Stealth scanning (less likely to be logged)
- Faster than TCP connect scans
- Default scan when run as root
</div>

### UDP Scan (-sU)

<div class="technique-box">
<h5>📡 UDP Scan</h5>
<p>Scans UDP ports. Slower but important for finding UDP services.</p>

<div class="command-block">
nmap -sU target.com
</div>

<strong>Use Cases:</strong>
- Finding UDP services (DNS, SNMP, DHCP)
- Often overlooked by defenders
- Combine with TCP scans for comprehensive coverage
</div>

---

## Port Specification

| Option | Description | Example |
|--------|-------------|---------|
| `-p 22` | Specific port | `nmap -p 22 target.com` |
| `-p 1-100` | Port range | `nmap -p 1-100 target.com` |
| `-p 22,80,443` | Multiple ports | `nmap -p 22,80,443 target.com` |
| `-p-` | All ports (1-65535) | `nmap -p- target.com` |
| `--top-ports 1000` | Top 1000 ports | `nmap --top-ports 1000 target.com` |

---

## Service Detection

### Version Detection (-sV)

<div class="command-block">
# Basic version detection
nmap -sV target.com

# Aggressive version detection
nmap -sV --version-intensity 9 target.com

# Light version detection
nmap -sV --version-intensity 2 target.com
</div>

### OS Detection (-O)

<div class="command-block">
# OS detection
nmap -O target.com

# Aggressive OS detection
nmap -O --osscan-guess target.com
</div>

<div class="warning-section">
<h4>⚠️ Warning</h4>
<p>OS detection can be noisy and may trigger security systems. Use with caution in production environments.</p>
</div>

---

## Timing and Performance

### Timing Templates

| Template | Speed | Stealth | Use Case |
|----------|-------|---------|----------|
| `-T0` (Paranoid) | Very