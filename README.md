# Phishing-URL-Detector
A beginner-friendly cybersecurity project built with Python that analyzes URLs for common phishing indicators and assigns a suspicion score based on the structure of the URL and the age of its domain.

  ## PROJECT OVERVIEW

Phish Guard CLI is a cybersecurity command-line tool that detects
phishing URLs using heuristic analysis.

Instead of relying on a database, it scores a URL based on suspicious
patterns like IP addresses, new domains, and phishing keywords.
This makes it perfect for students, analysts, and ethical hackers
practicing on Kali Linux.

Goal: Give anyone a fast "risk score" before they click a dangerous link.

  ## TECHNOLOGY USED

- Language: Python 3.8+
- Libraries: ipaddress, urllib, datetime, socket, whois
- Platform: Kali Linux, Windows, Mac
- Environment: Terminal / CLI
- Concepts: Heuristic Analysis, WHOIS Lookup, URL Parsing

## PROJECT STRUCTURE

phish-guard/
│
├── phishing_detector.py <- Main script with all logic
├── README.txt <- This file
└── requirements.txt <- python-whois dependency

  ## FEATURES

[1] URL Structure Analysis
    Scans for IP addresses, excessive subdomains, and hyphens.

[2] Phishing Keyword Detection
    Flags dangerous words like "login", "verify", "signin".

[3] Domain Age Analysis
    Uses WHOIS to check if the domain is brand new. New domains = high risk.

[4] Network-Safe Execution
    5-second WHOIS timeout so the tool won't freeze on Kali networks.

[5] Risk Scoring & Verdict
    Gives a score from 0-10 and a clear verdict: LOW, MEDIUM, or HIGH RISK.

[6] Detailed Reason Logging
    Prints exactly WHY a URL got its score.

  ## HOW IT WORKS

The tool runs 2 main checks on every URL and adds up the points.

Step 1: URL Structure Analysis
Step 2: Domain Age Analysis
Step 3: Total the score and give a verdict

  ## SUSPICION SCORING SYSTEM

Points are added for each red flag found:

| Check | Points | Reason |
|---------------------------------|--------|-----------------------------|
| Uses Raw IP Address | +2 | Phishers hide behind IPs |
| 3 or More Subdomains | +3 | e.g. a.b.c.paypal.com |
| Hyphen in Brand Name | +3 | e.g. pay-pal.com |
| Contains 'login/verify/signin' | +1 | Phishing tactic |
| Domain Age < 30 Days | +4 | New domains are suspicious |

VERDICT SCALE:
0-3 = 🟢 LOW RISK - Looks safe
4-6 = 🟡 MEDIUM RISK - Be cautious
7-10 = 🔴 HIGH RISK - Do NOT click

  ## URL STRUCTURE ANALYSIS

This module uses `urllib.parse` to break the URL apart.
It then checks:
1. Is the domain an IP? `ipaddress.ip_address()`
2. How many dots are in the domain? `domain.count('.')`
3. Is there a hyphen in the main brand name?
4. Are phishing keywords in the URL? `in url.lower()`

  ## DOMAIN AGE ANALYSIS

This module uses the `python-whois` library.
1. It does a WHOIS lookup on the domain
2. Gets the `creation_date`
3. Calculates age in days vs today
4. If < 30 days, it adds 4 points.
Note: Includes error handling for timeouts and blocked WHOIS on Kali.

  ## RUNNING THE PROJECT

PREREQUISITES:
1. Python 3.8 or higher
2. Install dependency:

   pip install python-whois

STEPS TO RUN:
1. Download `phishing_detector.py`
2. Open Terminal in the project folder
3. Run the script:

   python3 phishing_detector.py

CUSTOM USAGE:
To test your own URL, go to the bottom of the file and add:

   check_url("https://suspicious-link.com")

  ## WHAT I LEARNED

[1] Practical Web Security
    Learned how phishers structure malicious URLs to trick users.

[2] Python for Cybersecurity
    Used real modules like `whois`, `socket`, and `ipaddress` for OSINT.

[3] Building Heuristic Engines
    Learned to design a rule-based scoring system instead of ML.

[4] Robust Error Handling
    Learned to handle network failures and timeouts for real-world tools.

[5] CLI Tool Design
    Learned to make terminal output clean, readable, and actionable.

  ## CYBERSECURITY SKILL GAINED

- Threat Intelligence: Identifying phishing indicators
- OSINT: Using WHOIS for domain reconnaissance
- Secure Coding: Input validation and exception handling
- Risk Assessment: Turning technical findings into a risk score
- Tooling: Building a practical tool for a SOC analyst workflow

  ## PRACTICAL EXPERIENCE

This project simulates what a Tier-1 SOC analyst does daily:
"Analyst receives suspicious email link -> Run quick reputation check
-> Decide if it's safe".

It gave me hands-on experience with:
1. Breaking down attacker tactics
2. Writing code that works in restricted networks like Kali
3. Communicating risk clearly to a non-technical user

  ## HOW IT CAN BE IMPROVED

[1] Live Threat Feeds
    Integrate Google Safe Browsing API or VirusTotal API

[2] SSL Certificate Check
    Flag sites with no HTTPS or self-signed certificates

[3] Interactive CLI
    Loop to ask user: "Enter URL to scan:" instead of hardcoding

[4] Save Reports
    Export results to.csv or.pdf for documentation

[5] Levenshtein Distance
    Detect typosquatting: gooogle.com vs google.com

[6] GUI/Web Version
    Build with Flask or Tkinter for non-technical users

[7] Whitelist/Blacklist
    Add trusted domains to skip checks and known-bad domains

DISCLAIMER:
This tool is for educational and defensive purposes only. A low score
does NOT guarantee a URL is safe. Always use 2FA and common sense.

## Author
Eichie Benjamin

Cybersecurity student / Aspiring Cybersecurity Professional

Year: 11/9/2026
