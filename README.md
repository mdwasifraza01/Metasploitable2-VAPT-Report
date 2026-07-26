# Vulnerability Assessment & Penetration Testing (VAPT) Report
### Target: Metasploitable2 Lab Environment

---

## Document Control

| Parameter | Details |
| :--- | :--- |
| **Prepared By** | Md Wasif Raza |
| **Prepared For** | Self-Directed Penetration Testing Lab |
| **Target System** | 192.168.119.131 (Metasploitable2) |
| **Attacker Host** | 192.168.119.134 (Kali Linux) |
| **Engagement Type** | Internal, Unauthenticated Black-Box Assessment |
| **Assessment Dates** | July 23 – 26, 2026 |
| **Report Date** | July 26, 2026 |
| **Document Version** | 1.0 |

---

## Executive Summary
This report documents a penetration test performed against Metasploitable2, an intentionally vulnerable Linux virtual machine[cite: 6]. The assessment simulated an unauthenticated attacker with only network access to the target[cite: 6].

The engagement identified multiple critical vulnerabilities that allowed immediate, unauthenticated remote root access to the system through three independent attack paths: a backdoored FTP daemon, a hardcoded "ingreslock" backdoor shell, and a remote command injection flaw in Samba[cite: 6]. In addition, weak and default account passwords were recovered from the system's shadow file within seconds using an offline dictionary attack[cite: 6].

Root-level access (`uid=0`) was obtained via all of the following methods[cite: 6]:
1. **vsFTPd 2.3.4 Backdoor Command Execution** (Port 21 / 6200)[cite: 6]
2. **Ingreslock Backdoor Shell** (Port 1524)[cite: 6]
3. **Samba "username map script" Remote Command Execution** (Port 139/445)[cite: 6]
4. **Credential Reuse** (Cracked root password over SSH & Telnet)[cite: 6]

**Overall Risk Rating: CRITICAL**[cite: 6]

---

## 📄 Full Report Deliverable
The full PDF version of this report is available in the repository:
👉 [**Download Full VAPT Report PDF**](./Metasploitable2_Pentest_Report.pdf)

---

## Technical Findings Summary

| Finding | Severity | CVSS v3.1 | Primary Vector |
| :--- | :--- | :--- | :--- |
| FTP - vsFTPd 2.3.4 Backdoor | **Critical** | 10.0 | Remote Code Execution (Port 21/6200) |
| Samba usermap_script RCE | **Critical** | 10.0 | Remote Code Execution (Port 139/445) |
| Ingreslock Backdoor Shell | **Critical** | 10.0 | Unauthenticated Root Shell (Port 1524) |
| Weak / Default Credentials | **High** | 8.5 | Offline Hash Cracking / SSH & Telnet |
| Anonymous FTP Access | **Medium** | 5.3 | Information Disclosure (Port 21) |
| Telnet Cleartext Authentication | **Medium** | 5.9 | Credential Interception (Port 23) |

---

## Project Repository Structure
* `/scans/` — Raw Nmap port scan logs (`all_scanned_ports.txt`, `targeted_detailed.txt`).
* `Metasploitable2_Pentest_Report.pdf` — Polished PDF deliverable report.
