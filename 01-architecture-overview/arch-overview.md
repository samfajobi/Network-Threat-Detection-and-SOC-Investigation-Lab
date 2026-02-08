# 🏗️ Architecture Overview

This project implements a **network-focused threat detection and monitoring architecture** designed to simulate real-world SOC operations.  
It integrates **Suricata**, **Zeek**, and **Wazuh** to provide layered network visibility, alerting, and event correlation.

![Network Threat Detection Architecture](./01-lab-setup/network-diagram.png)

---

## 🎯 Architecture Goal

The primary goal of this architecture is to:

- Detect malicious network activity in real time
- Provide high-fidelity network telemetry
- Correlate network alerts into actionable security events
- Enable SOC-style investigation and incident response workflows

This setup closely mirrors how enterprise SOC environments monitor and respond to network threats.

---

## 🧩 Core Components

### 🔴 Attacker Machine – Kali Linux

- Simulates real-world adversary behavior
- Launches attacks such as:
  - Port scanning
  - SSH brute-force attempts
  - Web directory enumeration
  - Malware download simulations
  - Command-and-control beaconing
- Represents both external and internal threat actors

---




