# Subdomain Bruteforcing

## Summary

1. [Wordlist Selection and Process](#wordlist-selection)
2. [Tools](#tools)
3. [crt.sh lookup](#crtsh-lookup)

1. Wordlist Selection

- General Purpose
- Targeted
- Custom

2. Iteration and Querying

3. DNS Lookup

4. Filtering and Validation

# Tools

1. dnsenum

```bash 

dnsenum --enum inlanefreight.com -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -r

```

2. fierce
3. dnsrecon
4. amass
5. assetfinder
6. puredns

crt.sh lookup

```bash

curl -s "https://crt.sh/?q=%25.<domain>&output=json" | jq -r '.[].name_value' | sort -u

```

