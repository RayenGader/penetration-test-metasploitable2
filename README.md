# Penetration test - Metasploitable 2

![Kali](https://img.shields.io/badge/Kali%20Linux-557C94?style=flat-square&logo=kalilinux&logoColor=white)
![Nmap](https://img.shields.io/badge/Nmap-reconnaissance-4682B4?style=flat-square)
![Metasploit](https://img.shields.io/badge/Metasploit-exploitation-2596CD?style=flat-square)
![PTES](https://img.shields.io/badge/method-PTES%20%C2%B7%20OWASP%20%C2%B7%20NIST%20800--115-555?style=flat-square)

A full penetration test of **Metasploitable 2**, a deliberately vulnerable Linux target built
for security training. The engagement followed a structured methodology - reconnaissance,
enumeration, exploitation and post-exploitation - and ended with a risk analysis and a
prioritised remediation plan.

> Academic project, TEK-UP University. Carried out in an isolated lab against a target
> designed to be exploited. With **Zied Mellouli**, supervised by Mr. Houssem Eddine Hermassi.

---

## Scope

| | |
|---|---|
| Target | Metasploitable 2 (192.168.1.20) |
| Attacker | Kali Linux 2023.4 |
| Tooling | Nmap, Metasploit Framework, Netcat |
| Result | **5 vulnerabilities** - 2 critical, 2 high, 1 medium; root access achieved through several independent vectors |

## Methodology

1. **Reconnaissance** - host discovery, open ports, service and version detection (`nmap -sV -sC`).
2. **Enumeration** - users, default configurations, service banners.
3. **Exploitation** - for each confirmed vulnerability: exploit selection, configuration, initial shell, access verification.
4. **Post-exploitation** - privilege escalation and the impact of a persistent foothold.

## Findings

| # | Vulnerability | Service | CVE | CVSS | Severity |
|---|---|---|---|---|---|
| 1 | VSFTPD 2.3.4 backdoor command execution | FTP (21) | CVE-2011-2523 | 10.0 | **Critical** |
| 2 | Unauthenticated root bind shell | port 1524 | default config | 9.8 | **Critical** |
| 3 | PostgreSQL privilege escalation | PostgreSQL (5432) | CVE-2007-3278 | 8.8 | High |
| 4 | OpenSSH 4.7p1 vulnerability | SSH (22) | CVE-2010-4478 | 7.5 | High |
| 5 | Apache Tomcat Manager user enumeration | HTTP (8180) | misconfiguration | 5.3 | Medium |

**Also observed** during the service scan: Telnet, SMTP (Postfix), DNS (BIND 9.4.2) and
Apache httpd 2.2.8, all running outdated versions.

### Risk matrix

| Vulnerability | Likelihood | Impact | Overall risk |
|---|---|---|---|
| VSFTPD backdoor | High | Critical | **Critical** |
| Bind shell 1524 | High | Critical | **Critical** |
| PostgreSQL priv-esc | Medium | High | High |
| SSH CVE-2010-4478 | Medium | High | High |
| Tomcat enumeration | High | Medium | Medium |

## Remediation (summary)

| Priority | Action |
|---|---|
| Immediate | Upgrade VSFTPD to 3.0.3+; close port 1524 and remove the bind-shell process |
| Short term | PostgreSQL least privilege and strong auth; upgrade OpenSSH, key-based auth, no root password login |
| Medium term | Restrict the Tomcat manager interface, enforce MFA, monitor login attempts |
| Preventive | Patch-management process, regular vulnerability scans, an IDS, log monitoring and an incident-response procedure |

## What this project shows

- A repeatable penetration-testing methodology (PTES, OWASP Testing Guide, NIST SP 800-115) rather than isolated exploits.
- Mapping each finding to its CVE, a CVSS score and a business-impact statement.
- Remediation written so an administrator can act on it, with priorities and deadlines - the defensive half of offensive work.

> Screenshots (Nmap output, exploitation steps, privilege escalation) are in [`screenshots/`](screenshots/).
> The full report maps each one to a figure. The raw exploit commands are deliberately kept out of this
> README; the detail lives in the report, available on request.

---

**Rayen Gader** - Cyber Security Engineer, L2 SOC analyst ·
[Portfolio](https://rayengader.github.io/) · [LinkedIn](https://www.linkedin.com/in/rayengader/) · rayengader9@gmail.com
