# Web Application Security Labs

## Project Overview

This repository documents a series of hands-on labs focused on *web application security*. Each lab explores a common vulnerability class, demonstrates how it can be identified and exploited in a controlled lab environment, and discusses mitigation strategies.

The goal is to build practical understanding of how web applications are attacked and how defenders can identify, exploit, and fix vulnerabilities.

---

## Labs Index

| # | Lab | Vulnerability / Focus | Tools |
|---|-----|------------------------|-------|
| 01 | [SQL Injection](01-sql-injection.md) | Authentication bypass, boolean-based, time-based | Python, Flask, SQLite, Kali Linux |
| 02 | [Cross-Site Scripting (XSS)](02-xss-reflected-stored.md) | Reflected & Stored XSS | Xsser, Firefox |
| 03 | [Automated Scan with OWASP ZAP](03-zap-automated-scan.md) | Automated scanning & Path Traversal | OWASP ZAP, Nmap |

---

## Skills Demonstrated

- Identifying and exploiting SQL Injection vulnerabilities
- Understanding of Reflected vs Stored XSS
- Automated vulnerability scanning with OWASP ZAP
- Detecting Path Traversal vulnerabilities
- Generating and interpreting scan reports
- Understanding common mitigation strategies (parameterized queries, input validation, output encoding)
- Secure coding practices

---

## Tools Used

- Python (Flask)
- SQLite
- Kali Linux
- OWASP ZAP
- Xsser
- Nmap
- Firefox

---

## Ethical Disclaimer

This repository documents my personal learning journey using standard, publicly available security tools. All work was performed in isolated lab environments for educational purposes only.
