# 🏗️ Architecture Overview

![Network Threat Detection Architecture](../screenshots/Network-Threat-Detection-Project-01.png)

This project implements a **network-focused threat detection and monitoring architecture** designed to simulate real-world SOC operations.  
It integrates **Suricata**, **Zeek**, **Wireshark** and **Wazuh** to provide layered network visibility, alerting, and event correlation.

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

---

### 🌐 Zeek – Network Visibility & Behavioral Analysis

- Zeek focuses on **network behavior and metadata**, not signatures.
- It produces detailed logs such as:
  - `conn.log` (connections)
  - `dns.log` (DNS queries)
  - `http.log` (HTTP sessions)
  - `ssl.log` (TLS handshakes)
- These logs provide context around network activity and support threat hunting.

**Output:**
- Rich network telemetry
- Timeline reconstruction
- Detection of abnormal behavior

---

---

### 📦 Wireshark – Packet-Level Analysis

- Wireshark is used **strictly for packet capture and deep inspection**.
- It is **not used for detection or alerting**.
- Packet captures (PCAPs) are analyzed:
  - After an alert is triggered
  - During incident investigations
  - To validate Suricata and Zeek findings

**Use Cases:**
- Inspect malicious payloads
- Validate exploit attempts
- Reconstruct attack sessions
- Support forensic analysis

---

### Wazuh Agent
- Runs on the Ubuntu server
- Collects:
  - Suricata alert logs (`eve.json`)
  - Zeek network logs (`conn.log`, `dns.log`, etc.)
- Securely forwards logs to the Wazuh SIEM

### 🧠 Wazuh – SIEM & Event Correlation

- Wazuh acts as the **central SIEM platform**.
- It collects logs from:
  - Suricata alerts (`eve.json`)
  - Zeek network logs
  - System and agent logs from the Ubuntu sensor
- Wazuh correlates network and host-based events to:
  - Generate actionable alerts
  - Reduce false positives
  - Provide SOC dashboards and visualizations

**Capabilities:**
- Centralized log management
- Event correlation
- Alerting & dashboards
- Incident investigation support

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

1. Attacker generates malicious traffic from Kali Linux  
2. Traffic reaches the Ubuntu server  
3. Suricata inspects packets and generates alerts  
4. Zeek records detailed network activity  
5. Wazuh agent collects Suricata and Zeek logs  
6. Logs are forwarded to the Wazuh SIEM  
7. Events are correlated and visualized  
8. SOC analyst investigates and responds  

---

## 🛡️ Why This Architecture Works

- Layered detection (signature-based + behavioral)
- Network-first monitoring approach
- Centralized SIEM correlation
- SOC-aligned investigation workflow
- Realistic and extensible design

This architecture is intentionally designed to reflect **enterprise SOC network monitoring environments**, not just a basic lab setup.

---

## 🚀 Future Enhancements

- Integrate firewall and router telemetry
- Add threat intelligence feeds
- Develop custom Wazuh correlation rules
- Expand IPS enforcement scenarios
- Map detections to MITRE ATT&CK techniques

