Web Reconnaissance
==================

Active Reconnaissance
====================

| Technique            | Description                                                     | Example                                                                 | Tools                                           | Risk of Detection |
|----------------------|-----------------------------------------------------------------|-------------------------------------------------------------------------|-------------------------------------------------|-------------------|
| Port Scanning        | Identify open ports and services.                               | Scan a web server for ports 80/443 using Nmap.                          | Nmap, Masscan, Unicornscan                      | High              |
| Vulnerability Scanning | Probe for known vulnerabilities or misconfigurations.          | Run Nessus to check for SQLi or XSS flaws.                              | Nessus, OpenVAS, Nikto                          | High              |
| Network Mapping      | Map network topology and connected devices.                     | Use traceroute to reveal network hops to target.                        | Traceroute, Nmap                                | Medium–High       |
| Banner Grabbing      | Retrieve service banners for info.                              | Connect to port 80 and read HTTP banner.                                | Netcat, curl                                    | Low               |
| OS Fingerprinting    | Identify the target’s operating system.                         | Use Nmap `-O` to detect OS type.                                        | Nmap, Xprobe2                                   | Low               |
| Service Enumeration  | Determine versions of running services.                         | Use Nmap `-sV` to detect Apache or Nginx version.                       | Nmap                                            | Low               |
| Web Spidering        | Crawl site to find pages, directories, and files.               | Use Burp Suite Spider to map site structure.                            | Burp Suite Spider, OWASP ZAP Spider, Scrapy     | Low–Medium        |

Passive Reconnaissance
======================

| Technique              | Description                                                      | Example                                                                                     | Tools                                                                                  | Risk of Detection |
|------------------------|------------------------------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|-------------------|
| Search Engine Queries  | Use search engines to gather info on the target.                 | Search Google for "[Target Name] employees".                                               | Google, DuckDuckGo, Bing, Shodan                                                      | Very Low          |
| WHOIS Lookups          | Retrieve domain registration details.                            | WHOIS lookup to find registrant name, contacts, and name servers.                          | whois CLI, online WHOIS services                                                       | Very Low          |
| DNS                    | Analyse DNS records for subdomains and infrastructure.           | Use `dig` to enumerate subdomains.                                                         | dig, nslookup, host, dnsenum, fierce, dnsrecon                                        | Very Low          |
| Web Archive Analysis   | Review historical site snapshots for changes or clues.           | Use Wayback Machine to see older versions of a site.                                       | Wayback Machine                                                                        | Very Low          |
| Social Media Analysis  | Gather intel from social media platforms.                        | Search LinkedIn for employees’ roles and responsibilities.                                 | LinkedIn, Twitter, Facebook, OSINT tools                                               | Very Low          |
| Code Repositories      | Check public code repos for sensitive info or vulnerabilities.   | Search GitHub for exposed credentials in target-related code.                              | GitHub, GitLab                                                                         | Very Low          |
