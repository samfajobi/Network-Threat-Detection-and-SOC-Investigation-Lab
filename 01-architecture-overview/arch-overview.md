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

### 🟦 Network Sensor – Ubuntu Server

This system acts as the **monitored network asset** and hosts the network detection tools.

#### Suricata (IDS / IPS)
- Performs **signature-based and protocol-aware detection**
- Monitors live network traffic
- Generates alerts for:
  - Reconnaissance activity
  - Brute-force attempts
  - Exploit signatures
  - Suspicious traffic patterns
- Operates in:
  - IDS mode (detection only)
  - IPS mode (detection and blocking)

#### Zeek (Network Security Monitor)
- Provides **deep network visibility and metadata analysis**
- Focuses on behavioral logging rather than signatures
- Generates logs such as:
  - Connection logs
  - DNS queries
  - HTTP requests
  - SSL/TLS sessions
- Enables anomaly detection and traffic analysis

#### Wazuh Agent
- Runs on the Ubuntu server
- Collects:
  - Suricata alert logs (`eve.json`)
  - Zeek network logs (`conn.log`, `dns.log`, etc.)
- Securely forwards logs to the Wazuh SIEM

---

### 🟩 Wazuh SIEM & Dashboard

The Wazuh server functions as the **central security monitoring and correlation platform**.

- Ingests network alerts and logs
- Uses decoders and rules to parse events
- Correlates multiple events into incidents
- Generates alerts, dashboards, and timelines
- Provides centralized visibility for investigations

This component represents the **SOC SIEM layer**.

---

## 👨‍💻 SOC Analyst Workflow

Using the Wazuh dashboard, a SOC analyst can:

- Monitor Suricata IDS/IPS alerts
- Analyze Zeek network telemetry
- Correlate network activity across time
- Investigate suspicious behavior
- Perform incident response actions
- Document findings and lessons learned

---

## 🔁 Data Flow Summary

