# CV-Evidence
Production-grade homelab infrastructure deploying Proxmox VE, TrueNAS containers, automated n8n workflows, and active Wazuh SIEM security monitoring.
# Enterprise-Adjacent Homelab & Security Infrastructure

## Architecture Overview
This repository contains the architecture, configuration patterns, and deployment logic for my private home lab environment. The infrastructure is designed to test enterprise-grade virtualization, centralized storage provisioning, identity management (IAM), and security monitoring (SIEM).

### Hypervisor Layer (Proxmox VE)
The backbone of the lab runs on a **Proxmox VE** cluster, segmenting workloads based on function (Storage, Identity, Automation, and Security).

* **Node 100 (TrueNAS):** Centralized storage backend managing core datasets and containerized applications.
* **Node 102 (WazuH):** Dedicated SIEM for log aggregation, security monitoring, and endpoint audit analysis.
* **Node 103 (WServer):** Windows Server environment for Active Directory, Group Policy testing, and identity experiments.
* **Node 105 (N.O.M.A.D):** High-availability application and reverse-proxy deployment zone.

---

## Containerized Workloads & Services
The application layer is managed dynamically via containers, ensuring isolated environments for edge security and business automation.

| Application | Role / Function | Status |
| :--- | :--- | :--- |
| **Authelia** | Centralized Single Sign-On (SSO) & Multi-Factor Authentication (MFA) | In Production |
| **Nginx Proxy Manager** | Reverse proxy, SSL/TLS certificate management, and edge routing | In Production |
| **Fail2Ban** | Automated brute-force detection and IP banning at the edge | Active |
| **n8n** | Workflow automation engine linking internal APIs and administrative tasks | Active |
| **Uptime Kuma** | Real-time service monitoring and proactive incident alerting | Active |
| **Wazuh** | Security information and event management (SIEM) | Active |

---

## Configuration & Code Structure
To maintain a clean infrastructure-as-code layout, configuration examples are organized into the following directories:

* `/docker-compose/` - Sanitized YAML deployment files for core TrueNAS apps (Authelia, Nginx Proxy Manager, n8n).
* `/nginx-templates/` - Advanced proxy configurations showcasing secure headers and Authelia middleware integrations.
* `/scripts/` - Custom automation scripts.

---

## Security Posture
* **Zero Trust Access:** External entry points are restricted via Nginx Proxy Manager, forcing all traffic through Authelia MFA challenges.
* **Active Defense:** Fail2Ban monitors auth logs to dynamically drop malicious brute-force attempts before reaching app contexts.
* **Visibility:** System events and daemon logs are forwarded securely to the Wazuh SIEM collector for threat detection.
