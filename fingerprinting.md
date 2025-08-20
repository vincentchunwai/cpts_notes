# Fingerprinting


1. Targeted Attacks

2. Identifying Misconfigurations

3. Prioritising Targets

4. Building a Comprehensive Profile

# Fingerprinting techniques

- **Banner Grabbing**: Collecting information from service banners to identify software versions and configurations.

- **Analysing HTTP Headers**: HTTP headers can reveal server software, versions, and other details about the web application. [X-Powered-By](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Powered-By) is a common header that can indicate the technology stack used.

- **Probing for Specific Response**: Sending crafted requests to provoke specific responses that can reveal information about the server or application.

- **Analysing Page Content**: Examining the content of web pages for comments, metadata, or other clues that can indicate the technologies used.


# Tools for Fingerprinting

- **Wappalyzer**: A browser extension that identifies technologies used on websites, including frameworks, libraries, and analytics tools.

- **BuiltWith**: Web technology profiler that provides detailed information about the technologies used on a website.

- **WhatWeb**: A Command-line tool for website fingerprinting

- **Nmap**: A network scanning tool that can perform service detection and version detection to identify software running on hosts.

- **Netcraft**: A service that provides detailed information about the technologies used on a website, including server software, frameworks, and analytics tools.

- **wafw00f**: A tool for detecting and fingerprinting web application firewalls (WAFs) to understand their configurations and capabilities.

- **Nikto**: A web server scanner that can identify vulnerabilities and gather information about the technologies used on a web server.

## Install Nikto

```bash

sudo apt update && sudo apt install -y perl
git clone https://github.com/sullo/nikto
cd nikto/program
chmod +x nikto.pl

```

## Run Nikto

```bash

nikto -h <target> -Tuning b

```


