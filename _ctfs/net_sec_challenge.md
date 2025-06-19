---
layout: archive
author_profile: true
title: "Net Sec Challenge CTF Walkthrough"
description: "Write-up for the THM room Net Sec Challenge, covering the commands nmap, telnet, and hydra"
tags: [ctf, nmap, telnet, hydra, reconnaissance, tryhackme]
difficulty: "Medium"
category: "Network Security"
platform: "TryHackMe"
last_updated: 2025-06-18
header:
  overlay_color: "#000"
  overlay_filter: "0.4"
  overlay_image: /assets/images/ctf-banner.png
  height: 600px
  caption: >
    <div style="text-align: left; padding-left: 2rem; max-width: 600px;">
      <h1 style="margin-bottom: 0.3rem; color: #00ffd5; font-family: 'Fira Code', monospace;">Network Reconnaissance CTF</h1>
      <p style="margin-top: 0; color: #ccc; font-family: 'Fira Code', monospace;">Port scanning, service enumeration, and credential attacks</p>
    </div>
toc: true
toc_label: "Challenge Steps"
toc_icon: "flag"
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
  margin-top: 2rem !important;
  margin-bottom: 1rem !important;
}

.page__content p,
.content-wrapper p {
  color: #cccccc !important;
  font-family: 'Fira Code', monospace !important;
  line-height: 1.6 !important;
  margin-bottom: 1rem !important;
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
  margin: 2rem 0 !important;
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

/* Challenge Sections */
.challenge-section {
  background: rgba(0, 255, 213, 0.05);
  border-left: 4px solid #00ffd5;
  padding: 1.5rem;
  margin: 1.5rem 0;
  border-radius: 0 8px 8px 0;
}

.answer-section {
  background: rgba(76, 175, 80, 0.08);
  border-left: 4px solid #4caf50;
  padding: 1.5rem;
  margin: 1.5rem 0;
  border-radius: 0 8px 8px 0;
}

/* Command Blocks */
.command-block {
  background: rgba(0, 0, 0, 0.8);
  border: 1px solid #333;
  border-radius: 6px;
  padding: 1.5rem;
  font-family: 'Fira Code', monospace;
  color: #00ffd5;
  overflow-x: auto;
  line-height: 1.6;
  margin: 1rem 0;
}

/* Flag Boxes */
.flag-box {
  background: rgba(255, 193, 7, 0.1);
  border: 1px solid #ffc107;
  border-radius: 8px;
  padding: 1rem 1.5rem;
  margin: 1rem 0;
  text-align: center;
  font-family: 'Fira Code', monospace;
  font-weight: bold;
  color: #ffc107;
}

/* Methodology Boxes */
.method-box {
  background: rgba(255, 76, 240, 0.1);
  border: 1px solid #ff4cf0;
  border-radius: 8px;
  padding: 1.5rem;
  margin: 1.5rem 0;
}

.method-box h4 {
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
  margin-bottom: 1rem !important;
}

.page__content li,
.content-wrapper li {
  margin-bottom: 0.5rem;
  line-height: 1.5;
}

/* Target info */
.target-info {
  background: rgba(255, 87, 34, 0.1);
  border: 1px solid #ff5722;
  border-radius: 8px;
  padding: 1.5rem;
  margin: 2rem 0;
}

.target-info h4 {
  color: #ff5722 !important;
  margin-top: 0;
}

/* TryHackMe Link Box */
.thm-link {
  background: rgba(0, 255, 213, 0.1);
  border: 2px solid #00ffd5;
  border-radius: 8px;
  padding: 1.5rem;
  margin: 2rem 0;
  text-align: center;
}

.thm-link h4 {
  color: #00ffd5 !important;
  margin-top: 0;
}

/* Summary box */
.summary-box {
  background: rgba(0, 255, 213, 0.05);
  border: 1px solid #00ffd5;
  border-radius: 8px;
  padding: 1.5rem;
  margin: 2rem 0;
}

.summary-box h4 {
  color: #00ffd5 !important;
  margin-top: 0;
}
</style>

<div class="content-wrapper">

<h1>Challenge Overview</h1>

<div class="thm-link">
<h4>🚩 TryHackMe Challenge Room</h4>
<strong>Room Link:</strong> <a href="https://tryhackme.com/room/netsecchallenge" target="_blank">Net Sec Challenge</a><br>
<em>Complete the actual challenge on TryHackMe to get hands-on experience!</em>
</div>

<div class="target-info">
<h4>Target Information</h4>
<strong>Target IP:</strong> 10.10.28.88<br>
<strong>Objective:</strong> Perform network reconnaissance and answer questions about open ports, services, and hidden flags<br>
<strong>Tools Required:</strong> nmap, telnet, hydra
</div>

<p>This CTF focuses on fundamental network reconnaissance techniques including port scanning, service enumeration, and basic credential attacks. We'll systematically explore the target to answer each question.</p>

<hr>

<h2>Question 1: Highest Port Below 10,000</h2>

<div class="challenge-section">
<strong>Question:</strong> What is the highest port number being open less than 10,000?
</div>

<div class="method-box">
<h4>Methodology</h4>
<p>We need to scan ports below 10,000 to find the highest open port. Using nmap with the <code>-p -10000</code> switch will scan ports 1-9999.</p>
</div>

<div class="command-block">
<strong># Scan ports 1-9999</strong><br>
nmap 10.10.28.88 -p -10000
</div>

<div class="answer-section">
<strong>Analysis:</strong> The scan reveals several open ports, with the highest being port 8080.
</div>

<div class="flag-box">
Answer: 8080
</div>

<hr>

<h2>Question 2: Port Above 10,000</h2>

<div class="challenge-section">
<strong>Question:</strong> There is an open port outside the common 1000 ports; it is above 10,000. What is it?
</div>

<div class="method-box">
<h4>Methodology</h4>
<p>Now we scan ports above 10,000 using the range specification <code>10000-</code> which scans from 10000 to 65535.</p>
</div>

<div class="command-block">
<strong># Scan ports 10000-65535</strong><br>
nmap 10.10.28.88 -n -T4 -p 10000-
</div>

<div class="answer-section">
<strong>Analysis:</strong> The scan identifies an open port at 10021, which is running an FTP service on a non-standard port.
</div>

<div class="flag-box">
Answer: 10021
</div>

<hr>

<h2>Question 3: Total TCP Ports</h2>

<div class="challenge-section">
<strong>Question:</strong> How many TCP ports are open?
</div>

<div class="method-box">
<h4>Methodology</h4>
<p>Combining results from the previous two scans, we count all open TCP ports discovered.</p>
</div>

<div class="answer-section">
<strong>Analysis:</strong> From our scans, we identified the following open ports:
<ul>
<li>Port 22 (SSH)</li>
<li>Port 80 (HTTP)</li>
<li>Port 139 (NetBIOS)</li>
<li>Port 445 (SMB)</li>
<li>Port 8080 (HTTP-Alt)</li>
<li>Port 10021 (FTP)</li>
</ul>
<p>Total: 6 open TCP ports</p>
</div>

<div class="flag-box">
Answer: 6
</div>

<hr>

<h2>Question 4: HTTP Server Header Flag</h2>

<div class="challenge-section">
<strong>Question:</strong> What is the flag hidden in the HTTP server header?
</div>

<div class="method-box">
<h4>Methodology</h4>
<p>We'll use telnet to manually connect to the HTTP service and examine the server headers by sending a basic HTTP request.</p>
</div>

<div class="command-block">
<strong># Connect to HTTP service</strong><br>
telnet 10.10.28.88 80<br>
<br>
<strong># Send HTTP request</strong><br>
GET / HTTP/1.1<br>
Host: hacker<br>
<br>
<strong># Press Enter twice to send the request</strong>
</div>

<div class="answer-section">
<strong>Analysis:</strong> The HTTP response headers contain a custom server header with the hidden flag.
</div>

<div class="flag-box">
Flag: THM{web_server_****2}
</div>

<hr>

<h2>Question 5: SSH Server Header Flag</h2>

<div class="challenge-section">
<strong>Question:</strong> What is the flag hidden in the SSH server header?
</div>

<div class="method-box">
<h4>Methodology</h4>
<p>Similar to HTTP, we'll use telnet to connect to the SSH service and examine the banner information that's displayed upon connection.</p>
</div>

<div class="command-block">
<strong># Connect to SSH service</strong><br>
telnet 10.10.28.88 22
</div>

<div class="answer-section">
<strong>Analysis:</strong> Upon connecting to the SSH service, the server banner contains the hidden flag before the normal SSH protocol negotiation begins.
</div>

<div class="flag-box">
Flag: THM{9462*****339}
</div>

<hr>

<h2>Question 6: FTP Server Version</h2>

<div class="challenge-section">
<strong>Question:</strong> We have an FTP server listening on a nonstandard port. What is the version of the FTP server?
</div>

<div class="method-box">
<h4>Methodology</h4>
<p>We know from Question 2 that port 10021 is open. We'll use nmap with service version detection (<code>-sV</code>) to identify the FTP server version.</p>
</div>

<div class="command-block">
<strong># Service version detection on FTP port</strong><br>
nmap 10.10.28.88 -sV -p 10021
</div>

<div class="answer-section">
<strong>Analysis:</strong> The version scan reveals the FTP service is running vsftpd (Very Secure FTP Daemon) version 3.0.5.
</div>

<div class="flag-box">
Answer: vsftpd 3.0.5
</div>

<hr>

<h2>Question 7: FTP Account Flag</h2>

<div class="challenge-section">
<strong>Question:</strong> We learned two usernames using social engineering: eddie and quinn. What is the flag hidden in one of these two account files and accessible via FTP?
</div>

<div class="method-box">
<h4>Methodology</h4>
<p>We'll use hydra to perform brute force attacks against both usernames on the FTP service, then access the accounts to find the flag.</p>
</div>

<div class="command-block">
<strong># Brute force eddie's password</strong><br>
hydra -l eddie -P /usr/share/wordlists/rockyou.txt ftp://10.10.28.88:10021<br>
<strong># Result: Password is "jor***"</strong><br>
<br>
<strong># Brute force quinn's password</strong><br>
hydra -l quinn -P /usr/share/wordlists/rockyou.txt ftp://10.10.28.88:10021<br>
<strong># Result: Password is "and***"</strong>
</div>

<div class="command-block">
<strong># Connect to FTP with discovered credentials</strong><br>
ftp 10.10.28.88 10021<br>
<strong>User:</strong> quinn<br>
<strong>Password:</strong> [REDACTED]<br>
<br>
<strong># List files and download flag</strong><br>
ls<br>
get ftp_flag.txt<br>
exit<br>
<br>
<strong># Read the flag</strong><br>
cat ftp_flag.txt
</div>

<div class="answer-section">
<strong>Analysis:</strong> After successfully brute forcing both accounts, we find that quinn's account contains the flag file. The credentials follow common password patterns found in wordlists.
</div>

<div class="flag-box">
Flag: THM{3214****7098}
</div>

<hr>

<h2>Question 8: Web Challenge Flag</h2>

<div class="challenge-section">
<strong>Question:</strong> Browsing to http://10.10.28.88:8080 displays a small challenge that will give you a flag once you solve it. What is the flag?
</div>

<div class="method-box">
<h4>Methodology</h4>
<p>The web challenge likely requires a specific type of scan or technique. Based on the hint about displaying a challenge, we'll try different nmap scan types. A null scan (<code>-sN</code>) is often useful for bypassing simple firewalls.</p>
</div>

<div class="command-block">
<strong># Perform null scan</strong><br>
nmap 10.10.28.88 -sN
</div>

<div class="answer-section">
<strong>Analysis:</strong> The null scan technique triggers the web application to reveal the flag, likely as part of a scan detection mechanism or specific challenge requirement.
</div>

<div class="flag-box">
Flag: THM{f744****}
</div>

<hr>

<h2>Summary</h2>

<div class="summary-box">
<h4>Key Learning Points</h4>
<p>This challenge provided excellent practice with:</p>

<ul>
<li><strong>Port Scanning:</strong> Using nmap with different port ranges and scan types</li>
<li><strong>Service Enumeration:</strong> Identifying services and versions running on open ports</li>
<li><strong>Banner Grabbing:</strong> Using telnet to examine service headers and banners</li>
<li><strong>Credential Attacks:</strong> Using hydra for brute force attacks against FTP services</li>
<li><strong>Web Application Testing:</strong> Understanding how different scan types can trigger web applications</li>
</ul>

<p>The challenge demonstrates the importance of thorough reconnaissance in penetration testing and highlights various techniques for gathering information about target systems.</p>
</div>

<div class="thm-link">
<h4>🎯 Try It Yourself!</h4>
<strong>Complete the challenge:</strong> <a href="https://tryhackme.com/room/netsecchallenge" target="_blank">Net Sec Challenge on TryHackMe</a>
</div>

</div>