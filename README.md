# Ansible & GitLab

1. [Ansible Setup](#ansible-setup)
2. [Overview / Architectuur](#overview--architectuur)
3. [Inventory](#inventory)
4. [Configuratie SSH](#configuratie-ssh)
5. [Configuratie GitLab](#configuratie-gitlab)
6. [Commando's uitvoeren](#commandos-uitvoeren)
7. [Infrastructure as Code](#infrastructure-as-code)
8. [Ansible Playbooks](#ansible-playbooks)
9. [Uitrollen MySQL & Database](#uitrollen-mysql--database)


## Ansible Setup
De installatie van Ansible op Linux (in dit geval Ubuntu) servers is redelijk straight forward. Het verdient de aanbeveling om voor een specifieke user aan te maken voor "ansible werk". Ansible maakt gebruik van SSH om remote acties uit te voeren. We zullen dus de firewalls voor SSH open moeten stellen. 

Voer onderstaande commando's uit op alle servers in de farm. 
> NB: Als hardware rollout mogelijk is, bijvoorbeeld in een VMWare omgeving met fysiek toegankelijke servers, dan kan dit ook via Ansible uitgerold worden.

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

## Overview / Architectuur


## Inventory


## Configuratie SSH

Eerst moet een een SSH key gegenereerd worden om ssh-login naar de remote systemen mogelijk te maken. Deze key hebben we straks ook nodig om verbinding te maken met [GitLab](https://gitlab.com).

```bash
# as ansible user

# Generate a keypair
ssh-keygen

# Output: 
Generating public/private rsa key pair.
Enter file in which to save the key (/your_home/.ssh/id_rsa):

# press enter to save the key pair into the $HOME/.ssh directory
# If there is already a keypair, you will be asked to overwrite it. 
# The previous key *CANNOT BE USED ANYMORE*
# You should see the following prompt: 
Enter passphrase (empty for no passphrase):
# You can enter a passphrase for additional security

# Output will be something like this:
Your identification has been saved in /your_home/.ssh/id_rsa
Your public key has been saved in /your_home/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:/hk7MJ5n5aiqdfTVUZr+2Qt+qCiS7BIm5Iv0dxrc3ks user@host
The keys randomart image is:'
+---[RSA 3072]----+
|                .|
|               + |
|              +  |
| .           o . |
|o       S   . o  |
| + o. .oo. ..  .o|
|o = oooooEo+ ...o|
|.. o *o+=.*+o....|
|    =+=ooB=o.... |
+----[SHA256]-----+
```
Vervolgens moet de `$HOME/.ssh/id-rsa.pub` file naar de ontvangende user/host gekopieerd worden: 

```bash
# as ansible user
ssh-copy-id [username]@[host]

# example
# You will be prompted to enter the host fingerprint in to 
# your $HOME/.ssh/known-hosts file

# You also will be prompted for the password of the remote user. 

ssh-copy-id root@server-a
ssh-copy-id ansible@server-a

# Once this is achieved you can ssh into the remote system 
# without a password, hence, ansible can perform it's 
# tasks without interuption
ssh root@server-a
ssh ansible@server-a

```

## Configuratie GitLab


## Commando's Uitvoeren


## Infrastructure as Code


## Ansible Playbooks


## Uitrollen MySQL & Database