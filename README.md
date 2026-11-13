# 🛡️ Ansible Infrastructure Hardening

An Ansible-based automation project for **auditing and hardening** a multi-tier infrastructure including web servers, application servers, databases, Active Directory, firewalls (OPNsense), and SSH configurations.

---

## 🗺️ Infrastructure Architecture

![Infrastructure Architecture](docs/architecture.jpg)

> The infrastructure consists of a **DMZ** (web server behind a DMZ-router), an internal **production network** (App, DB, AD servers) managed through a Core Switch → Prod Switch hierarchy, and an **OPNsense Firewall** sitting between the internet (via Border-Router) and all internal segments. A **System Admin** workstation orchestrates everything via Ansible.

---

## 📁 Project Structure


```
ansible-infrastructure-hardening/
├── inventory/
│   ├── hosts.ini.example     # Template inventory (copy and fill in your values)
│   └── hosts.ini             # Your real inventory (git-ignored, never committed)
├── group_vars/               # Group-level variables
├── host_vars/                # Host-level variables
├── playbooks/
│   ├── ssh_audit.yml
│   ├── ss_hardening.yml
│   ├── system_audit.yml
│   ├── system_hardening.yml
│   ├── web_audit.yml
│   ├── web_hardening.yml
│   ├── app_audit.yml
│   ├── app_hardening.yml
│   ├── db_audit.yml
│   ├── db_hardening.yml
│   ├── ad_audit.yml
│   ├── ad_hardening.yml
│   ├── opnsense_audit.yml
│   └── opnsense_hardening.yml
├── roles/
│   ├── ssh_audit/
│   ├── ssh_hardening/
│   ├── system_baseline/
│   ├── system_web/
│   ├── system_app/
│   ├── system_db/
│   ├── system_ad/
│   └── system_opnsense/
└── reports/                  # Generated audit reports (git-ignored)
```

---

## 🎯 Scope

| Target           | Audit | Hardening |
|------------------|:-----:|:---------:|
| SSH              | ✅    | ✅        |
| Linux Baseline   | ✅    | ✅        |
| Web Server       | ✅    | ✅        |
| App Server       | ✅    | ✅        |
| Database Server  | ✅    | ✅        |
| Active Directory | ✅    | ✅        |
| OPNsense FW      | ✅    | ✅        |

---

## ⚙️ Requirements

- **Ansible** >= 2.12
- **Python** >= 3.8
- **pywinrm** (for Windows/AD targets): `pip install pywinrm`
- SSH access to Linux hosts
- WinRM enabled on Windows/AD hosts

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/<YOUR_USERNAME>/ansible-infrastructure-hardening.git
cd ansible-infrastructure-hardening
```

### 2. Set up your inventory

```bash
cp inventory/hosts.ini.example inventory/hosts.ini
# Edit hosts.ini and fill in your real IPs and credentials
```

> ⚠️ **Never commit `hosts.ini`** — it is listed in `.gitignore` to protect your credentials.

### 3. (Recommended) Use Ansible Vault for secrets

```bash
ansible-vault encrypt_string 'your_password' --name 'ansible_ssh_pass'
```

---

## 📋 Usage

### Run an audit

```bash
# SSH audit
ansible-playbook -i inventory/hosts.ini playbooks/ssh_audit.yml

# Full system audit
ansible-playbook -i inventory/hosts.ini playbooks/system_audit.yml

# Web server audit
ansible-playbook -i inventory/hosts.ini playbooks/web_audit.yml

# Database audit
ansible-playbook -i inventory/hosts.ini playbooks/db_audit.yml

# Active Directory audit
ansible-playbook -i inventory/hosts.ini playbooks/ad_audit.yml

# OPNsense firewall audit
ansible-playbook -i inventory/hosts.ini playbooks/opnsense_audit.yml
```

### Run hardening

```bash
# SSH hardening
ansible-playbook -i inventory/hosts.ini playbooks/ss_hardening.yml

# System baseline hardening
ansible-playbook -i inventory/hosts.ini playbooks/system_hardening.yml

# Web server hardening
ansible-playbook -i inventory/hosts.ini playbooks/web_hardening.yml

# Database hardening
ansible-playbook -i inventory/hosts.ini playbooks/db_hardening.yml

# Active Directory hardening
ansible-playbook -i inventory/hosts.ini playbooks/ad_hardening.yml

# OPNsense firewall hardening
ansible-playbook -i inventory/hosts.ini playbooks/opnsense_hardening.yml
```

---

## 🔐 Security Notes

- Real inventory files (`hosts.ini`) are **git-ignored** and must never be committed.
- Use **Ansible Vault** to encrypt sensitive variables in production.
- SSH private keys and vault password files are also git-ignored.

---

## 📄 License

This project is for educational and internal use. Adapt freely.
