# 🚀 Automated Switch Configuration Backup with Ansible and GitLab CI/CD 🛠️  

This project automates the backup of switch configurations from multiple sites and securely transfers the backup files to a centralized server. The workflow leverages Ansible for task automation and GitLab CI/CD pipelines for scheduling and orchestration.  

---

## 📋 Features  

- Automates configuration backups for switches across n sites.  
- GitLab CI/CD pipeline schedules the backup process monthly.  
- Transfers backup files to a central backup server via Samba.  

---

## 🛠️ Tools and Technologies  

- **Ansible**: For automating backup tasks.  
- **GitLab CI/CD**: For scheduling and orchestrating the pipeline.  
- **Samba**: For secure file transfer to the backup server.  

---

## 🔒 Using Ansible Vault for Secrets Management

This project uses Ansible Vault to securely store sensitive information such as credentials and configuration details. Follow the steps below to encrypt, manage, and use your secret files securely.


**🗂 Encrypting a Secret File**

1. Create the Secret File

   - Create a file to store your sensitive information (e.g., secrets.yml). Example content:

2. Encrypt the File with Ansible Vault

   - Run the following command to encrypt the file:

     ansible-vault encrypt secrets.yml

   - You will be prompted to create a password for the Vault. Keep this password secure, as it will be required for decryption.

**🔍 Viewing an Encrypted File**

   - To view the contents of an encrypted file:

     ansible-vault view secrets.yml

**✏️ Editing an Encrypted File**

   - To make changes to an encrypted file:

     ansible-vault edit secrets.yml

**🔓 Decrypting a File**

   - If you need to permanently decrypt a file:

     ansible-vault decrypt secrets.yml

⚠️ Caution: Decrypting the file will make its contents visible in plain text. Ensure it’s protected if you proceed with this step.

**🔑 Using the Vault in Ansible Playbooks**

1. Reference the encrypted file in your playbook. Example:


- name: Backup switch configurations
  hosts: switches
  vars_files:
    - secrets.yml
  tasks:
    ...

2. When running the playbook, specify the Vault password:

     ansible-playbook -i hosts.ini playbook.yml --ask-vault-pass

**💡 Automating Vault Password Management**

   - For automation or CI/CD pipelines, you can store the Vault password in as varaible in gitlab CI and use it  
     (e.g., $ANSIBLE_VAULT_PASSWORD ) and pass it to Ansible:

     ansible-playbook -i hosts-site1.ini playbook.yml  --vault-password-file <(echo "$ANSIBLE_VAULT_PASSWORD")


---

## 🚦 Workflow Overview  

1. **Backup Configurations**:  
   - Ansible playbooks connect to switches and retrieve their configurations.  

2. **Pipeline Scheduling**:  
   - GitLab CI/CD pipeline triggers monthly to execute the backup task.  

3. **Backup Transfer**:  
   - A secondary task in the pipeline uploads the backups to a backup server using Samba.  

---


## 🔧 Key Configuration

Inventory File (Hosts.ini)
List of switches:

[switches]

site1-switch   ansible_host=192.168.1.1

site2-switch   ansible_host=192.168.2.1
...


 Ansible Playbook (backup_switch.yml)
 Ensure the playbook matches your switch commands and saves configurations properly.


🌟 Benefits

Automated and Consistent: Reduces manual tasks and ensures reliable backups.
Centralized Management: Consolidates backups in a single location.
Secure and Scalable: Supports multiple sites with minimal changes.


📧 Support
If you encounter any issues or have questions, feel free to open an issue in this repository or contact the project maintainer.


