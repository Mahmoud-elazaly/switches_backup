# 🚀 Automated Switch Configuration Backup with Ansible and GitLab CI/CD 🛠️  

This project automates the backup of switch configurations from multiple sites and securely transfers the backup files to a centralized server. The workflow leverages **Ansible** for task automation and **GitLab CI/CD** pipelines for scheduling and orchestration.

---

## 📋 Features  

- Automates configuration backups for switches across **n sites**.  
- Schedules backups monthly via **GitLab CI/CD pipeline**, with adjustable timing.  
- Transfers backup files to a central server using **Samba**.  

---

## 🛠️ Tools and Technologies  

- **Ansible**: Automates backup tasks.  
- **GitLab CI/CD**: Schedules and orchestrates the pipeline.  
- **Samba**: Ensures secure file transfers to the backup server.  

---

## 🔒 Ansible Vault for Secrets Management

This project uses **Ansible Vault** to securely manage sensitive data like credentials and configurations.

### Key Commands  
- **Encrypt**: `ansible-vault encrypt secrets.yml` — Locks the file with a password.  
- **View**: `ansible-vault view secrets.yml` — Displays encrypted contents.  
- **Edit**: `ansible-vault edit secrets.yml` — Safely modifies the file.  
- **Decrypt**: `ansible-vault decrypt secrets.yml` — ⚠️ *Caution*: Reveals plain text.  

### Using in Playbooks  
Include the encrypted file:  
```yaml
- name: Backup Cisco Switch Configurations
  hosts: all
  connection: network_cli
  vars_files:
    - secrets.yml
```  
Run with password:  
- **Manual**: `ansible-playbook -i palm.ini palm_switches.yml --ask-vault-pass`  
- **Automated**: `ansible-playbook -i palm.ini palm_switches.yml --vault-password-file <(echo "$ANSIBLE_VAULT_PASSWORD")`  

### Automation Tip  
Store the Vault password in a CI/CD variable (e.g., `$ANSIBLE_VAULT_PASSWORD`) for seamless integration.

---

## 🔄 Workflow Breakdown  

1. **Configuration Retrieval**  
   - Ansible playbooks connect to switches at configured sites to retrieve their configurations.  

2. **Automated Scheduling**  
   - GitLab CI/CD pipelines execute the backup process monthly, with flexible scheduling options.  

3. **Centralized Storage**  
   - Backups are securely transferred to a central server via Samba.  

---

## 🌟 Benefits  

- **Automated and Consistent**: Minimizes manual effort and ensures reliable backups.  
- **Centralized Management**: Keeps all backups in one accessible location.  
- **Secure and Scalable**: Easily adapts to multiple sites with minimal adjustments.
