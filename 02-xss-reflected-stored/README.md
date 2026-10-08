# Lab 02: Cross-Site Scripting (XSS)

## Overview

In this lab, I explored *Cross-Site Scripting (XSS)* against a vulnerable web application. The lab covered two types of XSS: *Reflected* and *Stored*, and demonstrated how malicious JavaScript can be injected and executed in a victim's browser.

---

## Lab Environment

- *Operating System:* Linux
- *Target Application:* A custom vulnerable web application
- *Tools:* Xsser, Firefox, Kali Linux

---

## Background Concepts

### What is XSS?

Cross-Site Scripting (XSS) occurs when an attacker injects malicious scripts into web pages viewed by other users. The injected script executes in the victim's browser, allowing attackers to steal cookies, hijack sessions, or deface websites.

### Types of XSS

| Type | Description |
|------|-------------|
| Reflected | The payload is immediately returned by the server (e.g., via URL parameters) |
| Stored | The payload is saved on the server and served to other users |
| DOM-based | The payload executes via client-side JavaScript without touching the server |

### Why XSS Matters

- Can lead to *session hijacking* (stealing cookies).
- Can be used for *phishing* (fake login prompts).
- Can deface the website.
- Can be used to deliver malware.

### Prevention

- *Input validation:* Reject unexpected input.
- *Output encoding:* Encode output based on context (HTML, JS, URL).
- *Content Security Policy (CSP):* Restrict what scripts can run.
- *HttpOnly cookies:* Prevent JavaScript from accessing cookies.

---

## Lab Objectives

1. Identify XSS vulnerability in the application.
2. Exploit Reflected XSS.
3. Exploit Stored XSS.
4. Understand the difference between the two types.

---

## Methodology

### Step 1: Application Reconnaissance

Verified the target was up by pinging it. Then opened the application in Firefox and explored its sign-up and login functionality.

Created a test user and logged in to understand normal application behavior.

### Step 2: Automated Detection with Xsser

Used *Xsser*, an automated XSS detection tool, to scan the application:

text
xsser -u "http://demo.ine.local" -g "/profile/1?name=XSS"


Xsser identified a possible XSS vector in the name parameter of the profile page URL.

Step 3: Exploiting Reflected XSS

The profile page URL contained a name parameter:


http://demo.ine.local/profile/1?name=John+Doe


I replaced the value with a JavaScript payload:

html
<script>alert("XSS")</script>


Result: An alert box appeared in the browser — confirming the JavaScript executed.

Key observation: When I logged out and logged back in, the alert was gone. This confirmed the vulnerability was Reflected XSS — the payload was not stored on the server, only echoed back in the response.

Step 4: Exploiting Stored XSS

Next, I went to the Sign-Up page and injected the payload into the email field:

html
<script>alert("XSS")</script>


Completed the registration, then logged in with those credentials.

Result: The alert executed immediately after login.

Key observation: Even after logging out and logging back in, the alert continued to appear. This confirmed the vulnerability was Stored XSS — the payload was permanently saved on the server and served to every user visiting the page.

---

Key Observations

- Reflected XSS requires the victim to click a crafted link; the payload is not persisted.
- Stored XSS is more dangerous because it affects every user who visits the affected page.
- Even the email field during sign-up can be an injection point.
- Storing user input without proper encoding is the root cause of XSS.
- Automated tools (like Xsser) are useful but manual confirmation is essential.

---

Lessons Learned

- XSS is one of the most common web vulnerabilities.
- Both input validation and output encoding are required for proper mitigation.
- Stored XSS can persist across sessions and affect many users.
- Context-aware output encoding (HTML, JavaScript, URL) is critical.
- Tools like Xsser speed up detection but require analyst interpretation.

---

Tools Used

- Xsser
- Firefox
- Kali Linux
- Terminal

---

Ethical Disclaimer

This lab was performed in an isolated environment for educational purposes only. No real users or systems were affected.