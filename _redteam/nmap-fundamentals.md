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
| `-T0` (Paranoid) | Very Slow | Maximum | IDS evasion |
| `-T1` (Sneaky) | Slow | High | Stealth scanning |
| `-T2` (Polite) | Slow | Medium | Minimize bandwidth |
| `-T3` (Normal) | Normal | Low | Default timing |
| `-T4` (Aggressive) | Fast | Very Low | Fast networks |
| `-T5` (Insane) | Very Fast | None | Very fast networks |

<div class="command-block">
# Paranoid timing for maximum stealth
nmap -T0 -sS target.com

# Aggressive timing for speed
nmap -T4 -sS target.com

# Insane timing (may miss results)
nmap -T5 -sS target.com
</div>

### Custom Timing Options

<div class="command-block">
# Custom timing controls
nmap --min-rate 1000 --max-rate 5000 target.com

# Packet delays
nmap --scan-delay 1s target.com
nmap --max-scan-delay 2s target.com

# Parallelism
nmap --min-parallelism 50 --max-parallelism 100 target.com
</div>

---

## Host Discovery

### Ping Scans

<div class="technique-box">
<h5>🏓 Ping Scan Options</h5>
<p>Different methods to discover live hosts before port scanning.</p>

<div class="command-block">
# ICMP ping (default)
nmap -sn target.com

# TCP SYN ping
nmap -PS22,80,443 target.com

# TCP ACK ping
nmap -PA22,80,443 target.com

# UDP ping
nmap -PU53,161,137 target.com

# Skip ping (assume host is up)
nmap -Pn target.com
</div>
</div>

### ARP Ping

<div class="command-block">
# ARP ping for local network
nmap -PR 192.168.1.0/24

# List scan (no port scan)
nmap -sL 192.168.1.0/24
</div>

---

## Firewall Evasion

### Fragmentation

<div class="technique-box">
<h5>🧩 Packet Fragmentation</h5>
<p>Break packets into smaller fragments to evade firewalls.</p>

<div class="command-block">
# Fragment packets
nmap -f target.com

# Use specific MTU
nmap --mtu 24 target.com
</div>
</div>

### Decoy Scanning

<div class="technique-box">
<h5>🎭 Decoy Scanning</h5>
<p>Use decoy IP addresses to mask your real IP.</p>

<div class="command-block">
# Use decoy IPs
nmap -D 192.168.1.100,192.168.1.200,ME target.com

# Random decoys
nmap -D RND:10 target.com
</div>
</div>

### Source Port Spoofing

<div class="command-block">
# Use specific source port
nmap --source-port 53 target.com

# Use data length
nmap --data-length 25 target.com
</div>

---

## Nmap Scripting Engine (NSE)

### Script Categories

| Category | Description | Example |
|----------|-------------|---------|
| `auth` | Authentication scripts | `nmap --script auth target.com` |
| `broadcast` | Network broadcast discovery | `nmap --script broadcast` |
| `brute` | Brute force attacks | `nmap --script brute target.com` |
| `default` | Default scripts | `nmap -sC target.com` |
| `discovery` | Network discovery | `nmap --script discovery target.com` |
| `dos` | Denial of service | `nmap --script dos target.com` |
| `exploit` | Exploit scripts | `nmap --script exploit target.com` |
| `external` | External resource scripts | `nmap --script external target.com` |
| `fuzzer` | Fuzzing scripts | `nmap --script fuzzer target.com` |
| `intrusive` | Intrusive scripts | `nmap --script intrusive target.com` |
| `malware` | Malware detection | `nmap --script malware target.com` |
| `safe` | Safe scripts | `nmap --script safe target.com` |
| `version` | Version detection | `nmap --script version target.com` |
| `vuln` | Vulnerability detection | `nmap --script vuln target.com` |

### Common NSE Scripts

<div class="technique-box">
<h5>🔧 Popular NSE Scripts</h5>

<div class="command-block">
# HTTP enumeration
nmap --script http-enum target.com

# SMB enumeration
nmap --script smb-enum-shares target.com

# SSL/TLS information
nmap --script ssl-enum-ciphers target.com

# Vulnerability scanning
nmap --script vuln target.com

# Banner grabbing
nmap --script banner target.com
</div>
</div>

### Script Arguments

<div class="command-block">
# Pass arguments to scripts
nmap --script http-enum --script-args http-enum.basepath=/admin target.com

# Multiple arguments
nmap --script smb-brute --script-args userdb=users.txt,passdb=passwords.txt target.com
</div>

---

## Output Formats

### Standard Output Options

<div class="command-block">
# Normal output
nmap -oN scan_results.txt target.com

# XML output
nmap -oX scan_results.xml target.com

# Grepable output
nmap -oG scan_results.grep target.com

# All formats
nmap -oA scan_results target.com
</div>

### Verbosity Control

<div class="command-block">
# Increase verbosity
nmap -v target.com
nmap -vv target.com

# Debug output
nmap -d target.com
nmap -dd target.com

# Packet trace
nmap --packet-trace target.com
</div>

---

## Advanced Techniques

### TCP Window Scan

<div class="technique-box">
<h5>🪟 TCP Window Scan</h5>
<p>Differentiates open and closed ports by examining TCP window sizes.</p>

<div class="command-block">
nmap -sW target.com
</div>
</div>

### TCP Maimon Scan

<div class="technique-box">
<h5>📬 TCP Maimon Scan</h5>
<p>Sends FIN/ACK packets to evade certain firewalls.</p>

<div class="command-block">
nmap -sM target.com
</div>
</div>

### Idle Scan

<div class="technique-box">
<h5>😴 Idle Scan (Zombie Scan)</h5>
<p>Uses a zombie host to scan targets anonymously.</p>

<div class="command-block">
# Find zombie hosts
nmap -O -v 192.168.1.0/24

# Perform idle scan
nmap -sI zombie_host target.com
</div>
</div>

---

## Practical Examples

### Basic Network Discovery

<div class="command-block">
# Quick network discovery
nmap -sn 192.168.1.0/24

# Comprehensive host discovery
nmap -sn -PS22,80,443 -PA22,80,443 -PU53,161,137 192.168.1.0/24
</div>

### Web Server Enumeration

<div class="command-block">
# Web server scanning
nmap -sS -sV -p 80,443,8080,8443 --script http-enum,http-headers target.com

# SSL/TLS analysis
nmap -sS -p 443 --script ssl-enum-ciphers,ssl-cert target.com
</div>

### Database Server Scanning

<div class="command-block">
# Database ports
nmap -sS -sV -p 1433,3306,5432,1521,27017 target.com

# MySQL enumeration
nmap -sS -p 3306 --script mysql-info,mysql-enum target.com
</div>

### Windows Domain Enumeration

<div class="command-block">
# SMB enumeration
nmap -sS -p 445 --script smb-enum-shares,smb-enum-users,smb-os-discovery target.com

# Kerberos enumeration
nmap -sS -p 88 --script krb5-enum-users --script-args krb5-enum-users.realm=DOMAIN target.com
</div>

---

## Optimization Tips

<div class="tip-section">
<h4>💡 Performance Tips</h4>

**For Large Networks:**
- Use `-sn` for initial host discovery
- Scan top ports first with `--top-ports`
- Use timing templates appropriately (`-T3` or `-T4`)
- Consider using masscan for initial port discovery

**For Stealth:**
- Use `-T1` or `-T2` timing
- Fragment packets with `-f`
- Use decoy scanning `-D`
- Scan during business hours
- Randomize scan order with `--randomize-hosts`

**For Accuracy:**
- Use multiple scan types (`-sS -sU`)
- Enable version detection (`-sV`)
- Use appropriate scripts (`--script`)
- Verify results with different techniques
</div>

---

## Common Nmap Commands Reference

<div class="command-block">
# Quick scan
nmap target.com

# Comprehensive scan
nmap -sS -sV -O -A target.com

# Stealth scan
nmap -sS -T2 -f target.com

# UDP scan
nmap -sU --top-ports 1000 target.com

# Script scan
nmap -sC target.com

# Vulnerability scan
nmap --script vuln target.com

# Port range scan
nmap -p 1-10000 target.com

# Fast scan
nmap -F target.com

# Scan with output
nmap -oA results target.com
</div>

---

<div class="related-notes">
<h4>🔗 Related Notes</h4>
<ul>
<li><a href="/notes/service-enumeration">Service Enumeration Techniques</a></li>
<li><a href="/notes/stealth-scanning">Advanced Stealth Scanning</a></li>
<li><a href="/notes/firewall-evasion">Firewall Evasion Methods</a></li>
<li><a href="/notes/nse-scripts">NSE Script Development</a></li>
<li><a href="/notes/network-discovery">Network Discovery Techniques</a></li>
</ul>
</div>

<div class="warning-section">
<h4>⚠️ Legal Disclaimer</h4>
<p>Only use these techniques on networks you own or have explicit permission to test. Unauthorized scanning is illegal and unethical. Always follow responsible disclosure practices.</p>
</div>