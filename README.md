# 🛡️ SIEM Implementation and Its Use Cases

## 📌 Overview
This project demonstrates the implementation of a **Security Information and Event Management (SIEM)** system using **Wazuh** in a lab environment simulating a small business setup.  
The goal was to configure log collection, correlation rules, and real-time alerts for detecting common cyber threats, while ensuring a **cost-effective and scalable open-source solution**.

---

## 🚀 Features
- Centralized **Wazuh SIEM framework** with Manager, Agents, Indexer, and Dashboard.  
- **Custom rules & alerts** for:  
  - Brute-force attacks  
  - Unauthorized access attempts  
  - File Integrity Monitoring (FIM)  
  - USB-based Endpoint Detection & Response (EDR)  
- **Threat response workflows** with automated actions like IP blocking and notifications.  
- Secure communication between components using **AES/TLS encryption**.  
- Compliance-ready for standards such as **ISO 27001, HIPAA, GDPR**.  

---

## 🏗️ System Architecture

```
+---------------------+         +-------------------+
|  Windows/Linux      |  Logs   |                   |
|  Endpoints (Agents) +-------->+   Wazuh Manager   |
|  (Wazuh Agents)     |         |                   |
+---------------------+         +-------------------+
                                         |
                                         v
                               +-------------------+
                               |   Wazuh Indexer   |
                               | (OpenSearch)      |
                               +-------------------+
                                         |
                                         v
                               +-------------------+
                               | Wazuh Dashboard   |
                               |  (Web UI)         |
                               +-------------------+
```

This architecture ensures logs are collected at endpoints, analyzed by the Wazuh Manager, indexed for search, and visualized in real time through the Dashboard.

---

## 🛠️ Tools & Technologies
- **Wazuh** (SIEM platform)  
- **OpenSearch** (log indexing & search)  
- **Ubuntu Server** (Wazuh Manager, Indexer, Dashboard)  
- **Windows/Linux endpoints** (for testing agents)  
- **VirtualBox / VMware / Proxmox** (for virtualization)  

---

## ⚙️ Installation Guide

### 1. Update Your System
```bash
sudo apt update && sudo apt upgrade -y
```

### 2. Install Required Packages
```bash
sudo apt install curl apt-transport-https unzip wget gnupg -y
```

### 3. Add Wazuh Repository & Install Wazuh Manager
```bash
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo apt-key add -
echo "deb https://packages.wazuh.com/4.x/apt/ stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list
sudo apt update
sudo apt install wazuh-manager -y
sudo systemctl enable wazuh-manager
sudo systemctl start wazuh-manager
```

### 4. Install Wazuh Indexer (OpenSearch)
```bash
sudo apt install wazuh-indexer -y
sudo systemctl enable wazuh-indexer
sudo systemctl start wazuh-indexer
```

### 5. Install Wazuh Dashboard
```bash
sudo apt install wazuh-dashboard -y
sudo systemctl enable wazuh-dashboard
sudo systemctl start wazuh-dashboard
```

### 6. Install Wazuh Agent (on endpoints)
On **Linux** endpoint:  
```bash
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo apt-key add -
echo "deb https://packages.wazuh.com/4.x/apt/ stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list
sudo apt update
sudo apt install wazuh-agent -y
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

On **Windows** endpoint:  
Download and install agent from [Wazuh Agents Download](https://documentation.wazuh.com/current/installation-guide/installing-wazuh-agent/index.html).  

---

## 🔍 Testing Use Cases
- **Brute-Force Attack Detection:** Simulated SSH brute force → Alert triggered.  
- **File Integrity Monitoring (FIM):** Modified system files → Alerts and rollback.  
- **USB Detection with EDR:** Connected unauthorized USB → System detected & logged event.  

---

## 📈 Future Scope
- Integration with **ELK stack** for advanced analytics.  
- Machine learning-based anomaly detection.  
- Cloud-native deployment (AWS, Azure, GCP).  
- Scaling for enterprise environments.  

---

## 👨‍💻 Author
Developed by **Piyush Kumar Sahoo & Team**  
B.Tech Cybersecurity & Cyber Defense, Sri Sri University  
