# galileo-ansible

A demo Ansible Automation Platform (AAP) project showcasing automation playbooks and Event-Driven Ansible (EDA) integration for use with [Galileo](https://galileosuite.com) — an enterprise IT infrastructure monitoring platform built on Zabbix.

> **Note:** This repository is intended for demonstration purposes only. Playbooks and configurations provided here are not production-hardened and should be reviewed and adapted before use in production environments.

---

## Repository Structure

\```
galileo-ansible/
├── inventories/
│   └── hosts                        # Sample static inventory
├── playbooks/
│   ├── install-zabbix-agent.yml     # Install and configure Zabbix agent
│   └── install-galileo-agent.yml    # Install and configure Galileo agent
├── eda/
│   ├── rulebooks/
│   │   └── zabbix-alerts.yml        # EDA rulebook for Zabbix alert handling
│   └── playbooks/
│       └── remediation.yml          # Remediation playbook triggered by EDA
└── README.md
\```

---

## What's Included

### Playbooks

| Playbook | Description |
|---|---|
| `install-zabbix-agent.yml` | Installs and configures the Zabbix agent on target hosts |
| `install-galileo-agent.yml` | Installs and configures the Galileo monitoring agent on target hosts |

### Event-Driven Ansible (EDA)

This repo includes a demo EDA configuration that illustrates how Galileo/Zabbix alerts can trigger automated remediation workflows:

1. Galileo/Zabbix fires an alert via webhook
2. EDA rulebook receives and evaluates the event
3. Matching conditions trigger an AAP Job Template
4. Remediation playbook executes against the affected host

---

## Prerequisites

- Red Hat Ansible Automation Platform 2.6+
- Ansible EDA Controller
- Galileo / Zabbix environment with webhook support enabled
- Target hosts running RHEL, CentOS, or compatible Linux distribution

---

## Getting Started

### 1. Fork or clone this repository

\```bash
git clone https://github.com/<your-org>/galileo-ansible.git
\```

### 2. Add this repo as a Project in AAP

- Navigate to **Projects → Add**
- Set the SCM type to **Git**
- Enter your repository URL
- Save and sync

### 3. Configure your Inventory

Edit `inventories/hosts` to reflect your target environment, or create a dynamic inventory source pointing at your Zabbix or vCenter instance.

### 4. Create a Job Template

- Navigate to **Job Templates → Add**
- Select your Project and the desired playbook
- Assign your inventory and credentials
- Save and launch

### 5. Configure EDA (optional)

- Navigate to **EDA Controller → Rulebook Activations**
- Create a new activation pointing at `eda/rulebooks/zabbix-alerts.yml`
- Link it to your AAP Controller instance
- Configure your Zabbix webhook to point at the EDA webhook endpoint

---

## About Galileo

[Galileo](https://galileosuite.com) is an enterprise infrastructure monitoring platform, designed for organizations that need the power of total datacenter observability. This repository demonstrates how Galileo integrates with Ansible Automation Platform to close the loop between monitoring and automated remediation.

---

## Disclaimer

This repository is provided for demonstration and educational purposes only. The playbooks and configurations contained here are not intended for direct production use without review and adaptation to your specific environment.
