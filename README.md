# Project CyberWatch: SOC Infrastructure & Unified EDR Deployment

Built a centralized SOC monitoring environment using Wazuh SIEM/XDR on Ubuntu to monitor Windows 11 endpoint telemetry. Simulated brute-force attacks with PowerShell and validated detections through MITRE ATT&CK-aligned incident analysis.

## Architectural Vision
Project CyberWatch is a comprehensive Security Operations Center (SOC) engineering lab. The primary objective was to move beyond static log analysis and architect a **Live Telemetry Pipeline**. I engineered a centralized "Security Brain" using Wazuh (SIEM/XDR) on Ubuntu and established a high-fidelity monitoring bridge to a Windows 11 endpoint.

This project demonstrates the ability to deploy complex security infrastructure, manage cross-platform systems integration, and validate defense mechanisms through adversary simulation.

![Dashboard Overview](images/01_Infrastructure_Overview.png)
*Figure 1: The centralized CyberWatch Dashboard monitoring live endpoint telemetry.*

---

## The Engineering Stack
* **SIEM/XDR Platform:** Wazuh v4.x (Manager & Indexer)
* **Security Architecture:** Centralized Manager-Agent Model
* **Hypervisor:** UTM (Virtualized environment for Apple Silicon)
* **Infrastructure:** Ubuntu 22.04 LTS (Security Engine) | Windows 11 (Telemetry Source)
* **Networking:** Configured virtualized network bridges for inter-VM communication.

---

## Phase 1: Infrastructure Engineering & System Integration

### Centralized Management Deployment
I provisioned and hardened a Linux-based Wazuh Manager to serve as the project's central nervous system. This phase involved configuring the internal networking to ensure a stable communication path for incoming telemetry while resolving hardware-level virtualization hurdles.

### The Endpoint "Handshake"
The core challenge was establishing a persistent connection between the Windows 11 target and the Linux Manager.

* **The Problem:** Overcoming ARM64-specific driver instabilities and service enrollment failures.
* **The Solution:** Leveraged Administrative PowerShell to force-start security services, verify agent enrollment, and ensure stable telemetry ingestion.

![Agent Handshake Proof](images/02_Agent_Handshake.png)
*Figure 2: Successful handshake confirming the 'Wazuh' service is active on the Windows endpoint.*

---

## Phase 2: Adversary Simulation & Response

### Automated Brute Force Attack (PoC)
To validate the infrastructure’s detection logic, I executed an adversary simulation. Using an automated PowerShell loop, I targeted the SMB service with high-frequency authentication failures, intentionally triggering **Event ID 4625** (Logon Failure).

**Adversary Script:**
# Executing high-frequency authentication attempts to trigger SIEM correlation
1..15 | ForEach-Object { net use Z: \\127.0.0.1\c$ /user:Admin fake-password-$_ 2>$null }

![Attack Script Execution](images/03_Attack_Script.png)
*Figure 3: Execution of the PowerShell adversary simulation loop.*

### Incident Analysis & Threat Hunting
The CyberWatch pipeline successfully ingested the raw logs and triggered **Rule 60122** (Multiple logon failures). I performed a deep-dive analysis in the Threat Hunting module, correlating the hits to the **MITRE ATT&CK Framework: T1110 (Brute Force)**.

![SIEM Log Analysis](images/04_Threat_Hunting_Logs.png)
*Figure 4: Granular log analysis identifying the target account (Admin) and source IP (127.0.0.1).*

---

## Outcomes & Project Results

The primary success of this project was the transition from theoretical security concepts to a functional SOC lab environment with real-time telemetry visibility. Key outcomes include:

* **Improved Endpoint Visibility:** Built a real-time telemetry pipeline between Linux and Windows systems, enabling centralized monitoring similar to enterprise SOC environments.

* **Operational Resilience:** Resolved ARM64 virtualization and driver-level issues, ensuring stable and consistent communication between the Wazuh manager and endpoint agents.

* **Validated Detection Logic:** Tested SIEM rules through controlled adversary simulation. Identified and correlated **MITRE T1110 (Brute Force)** activity within 1,700+ generated events, confirming alert accuracy and detection reliability.

* **Technical Troubleshooting:** Strengthened skills in network debugging and service management, including configuration and validation of ports 1514/1515 in a virtualized environment.

---

## Key Skills & Competencies Demonstrated

### Security Engineering & Operations
* Deployment and configuration of Wazuh SIEM/XDR (Manager, Indexer, Dashboard)
* Setup and monitoring of Endpoint Detection & Response (EDR) agents
* Applied MITRE ATT&CK framework for threat detection and analysis

### Systems & Network Administration
* Cross-platform integration between Ubuntu (Linux) and Windows environments
* PowerShell scripting for system administration and controlled attack simulation
* Network troubleshooting and secure endpoint communication
* Linux system administration, service management, and log handling

---

## Summary

This project demonstrates practical SOC engineering skills, including SIEM deployment, endpoint monitoring, threat simulation, and log analysis in a controlled lab environment.

It also aligns with core cybersecurity principles covered in **CompTIA Security+**, particularly in areas such as threat detection, secure architecture design, and incident analysis.


---

## Connect with Me
* **LinkedIn:** [https://www.linkedin.com/in/sumanthkola/](https://www.linkedin.com/in/sumanthkola/)
* **Email:** sumanthkola.17@gmail.com
