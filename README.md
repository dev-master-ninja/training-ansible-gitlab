# Ansible & GitLab

1. Ansible Setup
2. Overview / Architectuur
3. Inventory
4. Configuratie SSH
5. Configuratie GitLab toegang
6. Commando's uitvoeren
7. Infrastructure as Code
8. Ansible Playbooks
9. Uitrollen MySQL & Database


## 1. Ansible setup
De installatie van Ansible op Linux (in dit geval Ubuntu) servers is redelijk straight forward. Het verdient de aanbeveling om voor een specifieke user aan te maken voor "ansible werk". Ansible maakt gebruik van SSH om remote acties uit te voeren. We zullen dus de firewalls voor SSH moeten openstellen. 

```bash
# As root user

adduser ansible
# add a password and fill in the other fields (or not).

# grant sudo permissions to user: 
usermod -aG sudo ansible

# OPTIONAL
# Setup a basic firewall (if not already done)
ufw app list

# Output
Available applications:
  OpenSSH

ufw allow OpenSSH

ufw enable

ufw status

# Output 
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)
```