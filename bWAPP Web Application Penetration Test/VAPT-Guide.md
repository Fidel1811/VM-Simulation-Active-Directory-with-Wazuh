# Environment Setup
## Update Kali Linux

Open a terminal and run:
```bash 
sudo apt update && sudo apt upgrade -y
```
## Install Docker & Docker Compose
```bash
sudo apt install docker.io docker-compose -y
sudo systemctl start docker
sudo systemctl enable docker
```

## Verify installation:
```bash 
docker --version
docker-compose --version
```

## Deploy bWAPP Using Docker
Create a new folder for bWAPP:
```bash 
mkdir ~/bWAPP && cd ~/bWAPP
```

## Create a docker-compose.yml file with this content:
```bash 
version: '3'
services:
  bWAPP:
    image: raesene/bwapp
    ports:
      - "8080:80"
```

## Run:
```bash 
docker-compose up -d
```

# Access in browser:
```bash
Go to http://localhost:8080/install.php
Follow the install wizard → database setup → login with default credentials:

Username: bee

Password: bug
```

## Testing Methodology (OWASP-Based)
We’ll use the VAPT workflow:

- Reconnaissance – Explore the web app manually.

- Vulnerability Identification – Test for OWASP Top 10 flaws.

- Exploitation – Demonstrate the impact.

- Documentation – Take screenshots, write findings.

- Remediation – Suggest fixes.

## Exploiting Common Vulnerabilities
## SQL Injection (SQLi)

- Log in to bWAPP → choose SQL Injection (GET/Search) from vulnerability list.

In the input box, enter:
```bash
' OR '1'='1
```
- Observe how all users are displayed.

- Take a screenshot of the result.

-- Lesson: Input not sanitized, backend database exposed.

## Cross-Site Scripting (XSS)

- Select Reflected XSS (GET) from the menu.

- In the text field, type:
```bash
<script>alert('Hacked by Esther')</script>
```
- If a pop-up appears, the site is vulnerable.

- Screenshot the alert.

-- Lesson: Application fails to sanitize user input → attacker can inject JavaScript

## Command Injection

- Select OS Command Injection from menu.

- Enter a valid IP, e.g.:
```bash
127.0.0.1; ls
```
- The command output (list of files) is displayed → proving arbitrary code execution.

- Screenshot output.

- Lesson: Application allows direct shell command injection.

## Cross-Site Request Forgery (CSRF)

- Select CSRF (Change Password).

- Open developer tools (F12 → Network tab).

- Capture the POST request made when changing the password.

- Copy the request into Burp Suite → Re-send it without logging in again.

- Notice password is changed without proper verification.

- Screenshot Burp request + successful password change.

- Lesson: No anti-CSRF tokens used → attacker can trick user into unwanted actions.

## Capturing with Burp Suite

- Open Burp Suite (preinstalled in Kali).

- Configure browser proxy to 127.0.0.1:8080.

- Visit bWAPP again → requests/responses will appear in Burp.

- Intercept, analyze, and forward to see how data flows.

- Take screenshots of intercepted traffic.
