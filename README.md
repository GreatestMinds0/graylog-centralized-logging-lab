# 🔐 Centralized Log Monitoring Lab — Graylog + Kali Linux + Ubuntu Server

[![Linux](https://img.shields.io/badge/OS-Linux-blue)](https://www.linux.org/) 
[![Docker](https://img.shields.io/badge/Docker-Container-blue?logo=docker)](https://www.docker.com/) 
[![Graylog](https://img.shields.io/badge/Graylog-Logging-orange)](https://www.graylog.org/)

---

## 📘 Project Overview

This project demonstrates a **centralized log collection and analysis environment** using:

- **Kali Linux** (log source / endpoint)  
- **Ubuntu Server** (Graylog, MongoDB, Elasticsearch/OpenSearch)  
- **rsyslog** for forwarding system logs  
- **Docker & Docker Compose** for containerized deployment  

Logs from endpoints are forwarded to Graylog, where they are indexed, stored, and searchable — providing a **SOC-like log monitoring and analysis capability**.

This project is based on a Haxcamp lab: [Centralized Logging Project](https://haxcamp.com/projects/8ba9c451-aebf-4c47-8889-bb7e84cb32b8/resources).

---

## 🎯 Objectives

- Configure Kali Linux to forward logs to a centralized server via rsyslog  
- Deploy and configure Graylog, MongoDB, and Elasticsearch/OpenSearch  
- Receive, index, and store logs in a structured format  
- Monitor and analyze security events like firewall blocks  
- Practice end-to-end troubleshooting of logging pipelines  

---

## 🛠️ Tools & Technologies

- **OS:** Kali Linux, Ubuntu Server  
- **Log Forwarding:** rsyslog  
- **SIEM / Log Management:** Graylog  
- **Data Storage:** MongoDB (configuration), Elasticsearch/OpenSearch (log indexing)  
- **Networking:** VirtualBox Bridged Networking  
- **Diagnostics & Testing:** tcpdump, logger, netstat / ss  
- **Containerization:** Docker, Docker Compose  

---

## 📝 Implementation Steps

1. **Network Setup**  
   - Configured VMs on the same subnet via VirtualBox Bridged Networking  
   - Verified connectivity using `ping` and captured network traffic with `tcpdump`

2. **Log Forwarding (Kali Linux)**  
   - Configured rsyslog to send logs to Graylog:  
     ```bash
     *.* @<Graylog-IP>:1514
     ```
   - Restarted rsyslog and confirmed messages were sent

3. **Graylog Deployment (Ubuntu Server)**  
   - Deployed Graylog in Docker with MongoDB and OpenSearch  
   - Created a **Syslog UDP input** on port 1514  
   - Enabled “Allow overriding source” to correctly identify log sources

4. **Log Validation & Troubleshooting**  
   - Sent test logs using `logger`  
   - Captured traffic with `tcpdump` to ensure arrival at Graylog  
   - Verified logs appeared in Graylog with correct metadata: source, facility, level, timestamp

5. **Result**  
   - Centralized logs from Kali Linux successfully indexed and searchable in Graylog  
   - Demonstrated structured logging, metadata parsing, and event monitoring

---

## 📄 Sample Log Entry

```json
{
  "source": "kali",
  "facility": "kernel",
  "level": 4,
  "message": "[UFW BLOCK] IN=eth0 OUT= ... SRC=192.168.1.1 DST=224.0.0.1 ... PROTO=2",
  "timestamp": "2025-12-04T05:07:33.026Z",
  "gl2_remote_ip": "192.168.1.166",
  "gl2_accounted_message_size": 508,
  "gl2_source_input": "6931135dfd38642a07d129af",
  "streams": ["000000000000000000000001"]
}
