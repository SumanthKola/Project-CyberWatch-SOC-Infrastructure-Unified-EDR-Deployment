# Project CyberWatch: SOC Infrastructure & Unified EDR Deployment

## 🏗️ Architectural Vision
Project CyberWatch is a comprehensive Security Operations Center (SOC) engineering lab. The primary objective was to move beyond static log analysis and architect a **Live Telemetry Pipeline**. I engineered a centralized "Security Brain" using Wazuh (SIEM/XDR) on Ubuntu and established a high-fidelity monitoring bridge to a Windows 11 endpoint. 

This project demonstrates the ability to deploy complex security infrastructure, manage cross-platform systems integration, and validate defense mechanisms through adversary simulation.

![Dashboard Overview](images/01_Infrastructure_Overview.png)
*Figure 1: The centralized CyberWatch Dashboard monitoring live endpoint telemetry.*

---

## 🛠️ The Engineering Stack
* **SIEM/XDR Platform:** Wazuh v4.x (Manager & Indexer)
* **Security Architecture:** Centralized Manager-Agent Model
* **Hypervisor:** UTM (Virtualized environment for Apple Silicon)
* **Infrastructure:** Ubuntu 22.04 LTS (Security Engine) | Windows 11 (Telemetry Source)
* **Networking:** Configured virtualized network bridges for inter-VM communication.

---

## 🔧 Phase 1: Infrastructure Engineering & System Integration

### Centralized Management Deployment
I provisioned and hardened a Linux-based Wazuh Manager to serve as the project's central nervous system. This phase involved configuring the internal networking to ensure a stable communication path for incoming telemetry while resolving hardware-level virtualization hurdles.

### The Endpoint "Handshake"
The core challenge was establishing a persistent connection between the Windows 11 target and the Linux Manager. 
* **The Problem:** Overcoming ARM64-specific driver instabilities and service enrollment failures.
* **The Solution:** Leveraged Administrative PowerShell to force-start security services, verify agent enrollment, and ensure 100% telemetry persistence.

![Agent Handshake Proof](images/02_Agent_Handshake.png)
*Figure 2: Successful handshake confirming the 'Wazuh' service is active on the Windows endpoint.*

---

## 🛡️ Phase 2: Adversary Simulation & Response

### Automated Brute Force Attack (PoC)
To validate the infrastructure’s detection logic, I executed an adversary simulation. Using an automated PowerShell loop, I targeted the SMB service with high-frequency authentication failures, intentionally triggering **Event ID 4625** (Logon Failure).

**Adversary Script:**
`powershell
# Executing high-frequency authentication attempts to trigger SIEM correlation
1..15 | ForEach-Object { net use Z: \\127.0.0.1\c$ /user:Admin fake-password-$_ 2>$null }

![Attack Script Execution](images/03_Attack_Script.png)
*Figure 3: Execution of the PowerShell adversary simulation loop.*

### Incident Analysis & Threat Hunting
The CyberWatch pipeline successfully ingested the raw logs and triggered **Rule 60122** (Multiple logon failures). I performed a deep-dive analysis in the **Threat Hunting** module, correlating the hits to the **MITRE ATT&CK Framework: T1110 (Brute Force)**.

![SIEM Log Analysis](images/04_Threat_Hunting_Logs.png)
*Figure 4: Granular log analysis identifying the target account (Admin) and source IP (127.0.0.1).*

---

## 📈 Outcomes & Professional Growth
* **Engineering vs. Analysis:** Successfully transitioned from a "Data Consumer" (Analyst) to a "System Creator" (Engineer) by building the entire log pipeline from scratch.
* **Cross-Platform Mastery:** Bridged communication between Linux and Windows architectures within a virtualized environment to create a unified security view.
* **Resourcefulness:** Resolved complex Apple Silicon virtualization conflicts and driver instabilities, ensuring stable deployment of enterprise-grade security tools.
* **Analytical Precision:** Successfully identified the specific target account (Admin) and source IP from 1,700+ raw telemetry events, demonstrating high-fidelity log correlation.

---
## 🔗 Connect with Me
* **LinkedIn:** [Your Link Here]
* **Email:** [Your Email Here]
