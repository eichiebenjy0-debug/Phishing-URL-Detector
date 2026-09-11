# Phishing-URL-Detector

1. PROJECT OVERVIEW

Phishing URL Detector is a Python command-line tool that analyzes
a URL and gives it a "Suspicion Score" from 0-10.

It checks for common phishing tricks like IP addresses, excessive
subdomains, brand-name hyphens, and brand-new domains. This helps
users quickly tell if a link is safe or risky before clicking.

Built and tested for Kali Linux / Python 3 environments.

2. FEATURES

[✓] URL Structure Analysis
    - Detects raw IP addresses instead of domains
    - Flags excessive subdomains (3+ dots)
    - Detects hyphens in brand names like pay-pal.com

[✓] Keyword Detection
    - Flags suspicious words: login, verify, signin in the URL

[✓] Domain Age Check
    - Uses WHOIS to check how old a domain is
    - Gives high risk score if domain is less than 30 days old
    - Has 5-second timeout to prevent freezing on Kali networks

[✓] Risk Verdict System
    - Score 0-3 : 🟢 LOW RISK - Looks safe
    - Score 4-6 : 🟡 MEDIUM RISK - Caution
    - Score 7-10 : 🔴 HIGH RISK - Do NOT click

[✓] Detailed Reporting
    - Prints each reason that increased the score
    - Clean, easy to read terminal output

3. WHAT I LEARNED

While building this project I learned and practiced:

1. Python Networking Modules:
    Used `socket`, `ipaddress`, and `whois` to inspect domains and
    handle network timeouts safely.

2. URL Parsing:
    Used `urllib.parse.urlparse` to break down a URL into domain,
    path, and other components for analysis.

3. Error Handling for Real Networks:
    Added try/except blocks and `socket.setdefaulttimeout(5)` so the
    script doesn't freeze when WHOIS is blocked on Kali.

4. Scoring/Heuristic Systems:
    Learned how to build a rule-based scoring system where each
    suspicious trait adds points to a total risk score.

5. Clean CLI UX:
    Learned to format terminal output with emojis, separators, and
    clear verdicts so results are easy to understand.

4. RUNNING THE PROJECT

REQUIREMENTS:
    Python 3.8+
    pip install python-whois

INSTALL:
    pip install python-whois

RUN:
    1. Save the code as phishing_detector.py
    2. Open terminal in the same folder
    3. Run the command:

       python3 phishing_detector.py

HOW TO USE:
    The script currently tests 3 URLs by default in the __main__ block.
    To test your own URL, edit the last lines and add:

       check_url("https://your-url-here.com")

EXAMPLE OUTPUT:
    🔍 Analyzing: http://paypal-secure.login.xyz.com

      Excessive subdomains (3 dots) (+3)
      ➖ Contains hyphens in brand name (+3)
       Contains 'login' or 'verify' (+1)
      Domain is 12 days old (+4)

    📊 TOTAL SUSPICION SCORE: 11 / 10
    🔴 VERDICT: HIGH RISK - Do NOT click!


5. HOW IT CAN BE IMPROVED

Here are ideas to take this project to the next level:

[1] SSL/TLS Check
    Add a check for HTTPS and invalid SSL certificates. Most phishing
    sites use fake HTTPS.

[2] Blacklist Integration
    Connect to Google Safe Browsing API or PhishTank API to check
    if the URL is already reported.

[3] Interactive Mode
    Instead of hardcoded URLs, let the user input URLs in a loop:
    `Enter URL to scan: `

[4] Export Results
    Add option to save results to CSV or TXT log file for reports.

[5] Website Content Scan
    Download the webpage and check for login forms + brand logo
    mismatch. E.g. URL says "apple" but page shows "bank".

[6] GUI Version
    Build a simple Tkinter or Flask web UI so non-technical users
    can paste a link and get a score.

[7] Whitelist
    Add a list of trusted domains like google.com, github.com to
    auto-mark as safe.

NOTES

Disclaimer: This tool uses heuristics. It does NOT guarantee 100%
accuracy. Always use common sense and 2FA when dealing with logins.

Built by: Eichie Benjamin
For: Cybersecurity / Kali Linux Practice
