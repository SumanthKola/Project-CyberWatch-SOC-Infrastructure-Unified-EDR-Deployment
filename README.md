# Project CyberWatch: SOC Infrastructure & Unified EDR Deployment

## Overview

Built a centralized SOC monitoring environment using Wazuh SIEM/XDR on Ubuntu to monitor Windows 11 endpoint telemetry. Simulated brute-force attacks with PowerShell and validated detections through MITRE ATT&CK-aligned incident analysis.

This project demonstrates hands-on experience in:
- SIEM deployment and configuration
- Cross-platform systems integration
- Threat detection engineering
- Security event correlation
- Windows and Linux administration
- SOC-style incident analysis

---

# Dashboard Overview

![CyberWatch Dashboard](images/dashboard.png)

**Figure 1:** Centralized CyberWatch dashboard monitoring live endpoint telemetry.

---

# The Engineering Stack

| Component | Technology |
|---|---|
| SIEM/XDR Platform | Wazuh v4.x |
| Security Architecture | Centralized Manager-Agent Model |
| Hypervisor | UTM (Apple Silicon Virtualization) |
| Infrastructure | Ubuntu 22.04 LTS + Windows 11 |
| Networking | Virtualized bridge networking |
| Scripting | PowerShell |

---

# Project Structure

```text
Project-CyberWatch/
│
├── images/
│   ├── dashboard.png
│   ├── handshake.png
│   ├── attack-execution.png
│   └── threat-analysis.png
│
├── scripts/
│   └── brute-force-simulation.ps1
│
├── configs/
│   └── wazuh-agent-config.txt
│
└── README.md
```

---

# Phase 1: Infrastructure Engineering & System Integration

## Centralized Management Deployment

Provisioned and configured a Linux-based Wazuh Manager to serve as the project's centralized security monitoring platform. Configured internal VM networking to establish stable communication between Windows endpoints and the SIEM infrastructure.

Key tasks included:
- Wazuh Manager installation and configuration
- Virtualized network bridge setup
- Port communication validation (1514/1515)
- Linux service management and troubleshooting
- Cross-platform endpoint integration

---

## The Endpoint "Handshake"

The primary challenge involved establishing stable communication between the Windows 11 endpoint and the Ubuntu-based Wazuh Manager.

### Challenges
- ARM64 virtualization driver instability
- Wazuh agent enrollment failures
- Windows service startup issues

### Solutions
- Used Administrative PowerShell for service management
- Verified Wazuh agent enrollment manually
- Validated consistent telemetry ingestion
- Troubleshot endpoint communication failures

![Agent Handshake](images/handshake.png)

**Figure 2:** Successful Windows endpoint enrollment and active Wazuh service communication.

---

# Phase 2: Adversary Simulation & Detection Engineering

## Automated Brute Force Attack Simulation

To validate SIEM detection logic, a PowerShell-based brute-force simulation was executed against the SMB service. The attack intentionally generated multiple Windows Event ID 4625 authentication failures.

### PowerShell Adversary Simulation

```powershell
1..15 | ForEach-Object {
    net use Z: \\127.0.0.1\c$ /user:Admin fake-password-$_ 2>$null
}
```

![Attack Simulation](images/attack-execution.png)

**Figure 3:** Execution of the PowerShell brute-force simulation.

---

# Incident Analysis & Threat Hunting

The CyberWatch pipeline successfully ingested endpoint logs and triggered Wazuh Rule 60122 for multiple authentication failures.

Threat hunting analysis identified:
- Source IP address
- Targeted user account
- Authentication failure patterns
- Correlated attack timeline

Mapped detection to:
- MITRE ATT&CK Technique: **T1110 – Brute Force**

![Threat Hunting Analysis](images/threat-analysis.png)

**Figure 4:** Wazuh threat hunting analysis identifying brute-force activity.

---

# Key Skills Demonstrated

- SIEM/XDR deployment and configuration
- Windows endpoint monitoring
- Linux server administration
- PowerShell scripting
- Threat detection engineering
- MITRE ATT&CK framework mapping
- Windows Event ID analysis
- Security event correlation
- Cross-platform troubleshooting
- Network communication debugging

---

# Outcomes & Learning

Through this project, I successfully:

- Engineered a centralized SOC-style telemetry pipeline
- Integrated Windows and Linux systems for security monitoring
- Simulated adversary behavior to validate detection logic
- Performed event correlation and incident investigation
- Troubleshot virtualization and networking challenges on ARM64 architecture
- Analyzed 1,700+ security events to isolate malicious authentication activity

---

# Future Improvements

Planned enhancements for future iterations:

- Integrate Sysmon for enhanced Windows telemetry
- Add Suricata IDS integration
- Develop custom Wazuh detection rules
- Automate agent deployment with PowerShell
- Expand monitoring to multiple Windows endpoints
- Implement automated alert escalation workflows

---

# Technical Competencies

## Security Operations
- Wazuh SIEM/XDR
- Threat hunting
- Event correlation
- Alert validation

## Operating Systems
- Ubuntu 22.04 LTS
- Windows 11

## Networking
- Virtual bridge networking
- Port communication troubleshooting
- Endpoint connectivity validation

## Scripting & Automation
- PowerShell scripting
- Windows service management

## Security Frameworks
- MITRE ATT&CK
- Windows Event ID analysis

---

# Connect With Me

- LinkedIn: https://www.linkedin.com/in/sumanthkola/
- Email: sumanthkola.17@gmail.com

---

# About

A full-scale SOC engineering lab focused on centralized SIEM monitoring, endpoint telemetry ingestion, attack simulation, and threat detection analysis using Wazuh and Windows endpoints.
