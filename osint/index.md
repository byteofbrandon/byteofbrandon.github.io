---
layout: archive
author_profile: true
header:
  overlay_color: "#000"
  overlay_filter: "0.4"
  overlay_image: /assets/images/banner.png
---

<div style="text-align: left; margin-bottom: 2rem;">
  <h1 style="margin-bottom: 0.3rem; color: #00ffd5; font-family: 'Fira Code', monospace;">OSINT Resources</h1>
  <p style="margin-top: 0; color: #ccc; font-family: 'Fira Code', monospace;">Essential tools for open source intelligence gathering</p>
</div>

<div class="osint-grid">
  <div class="osint-card">
    <h2><a href="https://www.shodan.io/" target="_blank">Shodan</a></h2>
    <p><strong>Description:</strong> Internet-connected device search engine that scans and indexes devices across the web.</p>
    <p><strong>Use Cases:</strong></p>
    <ul>
      <li>Discovering exposed databases, webcams, and IoT devices</li>
      <li>Network reconnaissance and vulnerability assessment</li>
      <li>Identifying misconfigured services and open ports</li>
      <li>Threat hunting and monitoring for exposed assets</li>
    </ul>
  </div>

  <div class="osint-card">
    <h2><a href="https://dnsdumpster.com/" target="_blank">DNSdumpster</a></h2>
    <p><strong>Description:</strong> Free domain research tool for discovering hosts related to a domain through DNS records.</p>
    <p><strong>Use Cases:</strong></p>
    <ul>
      <li>Mapping subdomains and DNS infrastructure</li>
      <li>Identifying potential attack vectors</li>
      <li>Reconnaissance for penetration testing</li>
      <li>Understanding target organization's digital footprint</li>
    </ul>
  </div>

  <div class="osint-card">
    <h2><a href="https://tineye.com/" target="_blank">TinEye</a></h2>
    <p><strong>Description:</strong> Reverse image search engine that finds where images appear across the web.</p>
    <p><strong>Use Cases:</strong></p>
    <ul>
      <li>Verifying authenticity of images in investigations</li>
      <li>Tracking image usage and copyright infringement</li>
      <li>Social media profile verification</li>
      <li>Identifying fake accounts using stolen photos</li>
    </ul>
  </div>

  <div class="osint-card">
    <h2><a href="https://www.exploit-db.com/google-hacking-database" target="_blank">Google Hacking Database</a></h2>
    <p><strong>Description:</strong> Collection of Google search queries (dorks) to find sensitive information and vulnerabilities.</p>
    <p><strong>Use Cases:</strong></p>
    <ul>
      <li>Finding exposed files, directories, and databases</li>
      <li>Discovering vulnerable web applications</li>
      <li>Identifying misconfigured servers and services</li>
      <li>Gathering intelligence on target organizations</li>
    </ul>
  </div>

  <div class="osint-card">
    <h2><a href="https://haveibeenpwned.com/" target="_blank">Have I Been Pwned</a></h2>
    <p><strong>Description:</strong> Service that checks if email addresses have been compromised in known data breaches.</p>
    <p><strong>Use Cases:</strong></p>
    <ul>
      <li>Checking if credentials are compromised</li>
      <li>Investigating data breach impacts</li>
      <li>Validating email addresses in investigations</li>
      <li>Security awareness and password hygiene</li>
    </ul>
  </div>

  <div class="osint-card">
    <h2><a href="https://search.censys.io/" target="_blank">Censys</a></h2>
    <p><strong>Description:</strong> Search engine for Internet-connected devices with detailed certificate and service information.</p>
    <p><strong>Use Cases:</strong></p>
    <ul>
      <li>Certificate transparency monitoring</li>
      <li>Network asset discovery and inventory</li>
      <li>SSL/TLS configuration analysis</li>
      <li>Tracking infrastructure changes over time</li>
    </ul>
  </div>

  <div class="osint-card">
    <h2><a href="https://intelx.io/tools?tab=username" target="_blank">Intelligence X</a></h2>
    <p><strong>Description:</strong> Search engine and data archive for OSINT with username search capabilities.</p>
    <p><strong>Use Cases:</strong></p>
    <ul>
      <li>Username enumeration across platforms</li>
      <li>Historical data and leak searches</li>
      <li>Social media profile discovery</li>
      <li>Digital footprint analysis</li>
    </ul>
  </div>

  <div class="osint-card">
    <h2><a href="https://www.virustotal.com/gui/home/upload" target="_blank">VirusTotal</a></h2>
    <p><strong>Description:</strong> Multi-engine malware analysis service that scans files and URLs for threats.</p>
    <p><strong>Use Cases:</strong></p>
    <ul>
      <li>Malware analysis and threat intelligence</li>
      <li>URL and file reputation checking</li>
      <li>Incident response and forensics</li>
      <li>IOC (Indicators of Compromise) validation</li>
    </ul>
  </div>

  <div class="osint-card">
    <h2><a href="https://www.exploit-db.com/" target="_blank">Exploit Database</a></h2>
    <p><strong>Description:</strong> Archive of public exploits and corresponding vulnerable software.</p>
    <p><strong>Use Cases:</strong></p>
    <ul>
      <li>Vulnerability research and analysis</li>
      <li>Penetration testing and red team operations</li>
      <li>Security patch prioritization</li>
      <li>Threat intelligence and CVE research</li>
    </ul>
  </div>

  <div class="osint-card">
    <h2><a href="https://osintframework.com/" target="_blank">OSINT Framework</a></h2>
    <p><strong>Description:</strong> Comprehensive collection of OSINT tools organized by category and use case.</p>
    <p><strong>Use Cases:</strong></p>
    <ul>
      <li>Discovering new OSINT tools and techniques</li>
      <li>Structured approach to intelligence gathering</li>
      <li>Training and education resource</li>
      <li>Quick reference for investigation workflows</li>
    </ul>
  </div>
</div>

<div style="margin-top: 3rem; padding: 1.5rem; background-color: #1a1a1a; border-left: 4px solid #00ffd5; border-radius: 4px;">
  <h3 style="margin-top: 0;">⚠️ Ethical Use Notice</h3>
  <p style="margin-bottom: 0;">These tools are powerful and should be used responsibly. Always ensure you have proper authorization before conducting any reconnaissance or testing activities. Respect privacy, follow applicable laws, and adhere to ethical hacking principles.</p>
</div>

<style>
h1, h2, h3, h4 {
  color: #00ffd5;
  font-family: 'Fira Code', monospace;
}

p, li {
  color: #cccccc;
  font-family: 'Fira Code', monospace;
  line-height: 1.6;
}

a {
  color: #00ffd5;
  text-decoration: underline;
  transition: color 0.3s ease;
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

body .osint-grid {
  display: grid !important;
  grid-template-columns: repeat(2, 1fr) !important;
  gap: 2rem !important;
  margin-top: 2rem !important;
  width: 100% !important;
  box-sizing: border-box !important;
}

body .osint-card {
  background-color: #1a1a1a !important;
  padding: 2rem !important;
  border-radius: 8px !important;
  border: 1px solid #333 !important;
  transition: border-color 0.3s ease, box-shadow 0.3s ease !important;
  margin-bottom: 0 !important;
  width: 100% !important;
  box-sizing: border-box !important;
}

.osint-card:hover {
  border-color: #00ffd5;
  box-shadow: 0 0 15px rgba(0, 255, 213, 0.2);
}

.osint-card h2 {
  margin-top: 0;
  margin-bottom: 1rem;
  font-size: 1.2rem;
}

.osint-card ul {
  margin: 0.5rem 0;
  padding-left: 1.5rem;
}

.osint-card li {
  margin-bottom: 0.3rem;
}

.osint-card strong {
  color: #ff4cf0;
}

@media (max-width: 768px) {
  body .osint-grid {
    grid-template-columns: 1fr !important;
    gap: 1.5rem !important;
  }
  
  body .osint-card {
    padding: 1rem !important;
  }
}

@media (min-width: 769px) {
  body .osint-grid {
    grid-template-columns: repeat(2, 1fr) !important;
    gap: 2rem !important;
  }
}

@media (min-width: 1400px) {
  body .osint-grid {
    max-width: none !important;
    margin: 2rem auto !important;
  }
  
  body .archive,
  body #main,
  body .initial-content {
    max-width: none !important;
    width: 90% !important;
    margin: 0 auto !important;
  }
}
</style>