# Ansible Installation On AWS Ubuntu 22.04/20.04/18.04

Ansible is an open source tool that you can use to automate your AWS deployments. You can use it to define, deploy, and manage applications and services using automation playbooks. These playbooks enable you to define configurations once and deploy those configurations consistently across environments. Safe automation.
## [Follow Video Tutorial](#)

## Prerequisites
1.An AWS EC2 Instance (ubuntu 22.04/20.04/18.04)

## Installation

Run 
This Command
```bash
sudo apt update -y
```
```bash
sudo apt upgrade -y
```
```bash
sudo apt install software-properties-common
```
```bash
sudo add-apt-repository --yes --update ppa:ansible/ansible
```
```bash
sudo apt install ansible
```
#### Check Ansible version And Configuration Path
![Example](https://github.com/ritikvirus/Ansible/blob/main/Images/ubuntu/ansible_checking.PNG)
## Now Open Ansible Configuration File
```bash
sudo vim /etc/ansible/ansible.cfg
```
1. Write [defaults]
```bash
[defaults]
```
2. Write inventory = /etc/ansible/hosts
```bash
inventory = /etc/ansible/hosts
```
3. Write sudo_user = root
```bash
sudo_user = root
```
4. Write host_key_checking = False
```bash
host_key_checking = False
```

![Example2](https://github.com/ritikvirus/Ansible/blob/main/Images/ubuntu/ansible_configuration.PNG)

### Now Set Group And Node IPs
```bash
sudo vim /etc/ansible/hosts
```
Make Group **[groupname]**  
Press Enter Give Node IPs
![Example4](https://github.com/ritikvirus/Ansible/blob/main/Images/give_group_name_and_ips.PNG)
### Generate SSH KEY by Using This Command
```bash
ssh-keygen
```
![Example5](https://github.com/ritikvirus/Ansible/blob/main/Images/ssh-keygen.PNG)
### Now Go To ~ Directory
```bash
cd ~
```
```bash
cd .ssh
```
```bash
sudo vim id_rsa.pub
```
![Example6]()
**Copy SSH KEY From Master And Past Nodes**  
![Example6](https://github.com/ritikvirus/Ansible/blob/main/Images/copyMaster_key.PNG)
# All Nodes System Use These Steps
### Type These Commands in Nodes System
```bash
sudo apt update -y
```
```bash
cd ~
```
```bash
cd .ssh
```
```bash
sudo vim authorized_keys
```
***Past Copied SSH KEY From Master Past in Node***  
Go to last line then press enter then past your copied master system ssh Key
![Example7](https://github.com/ritikvirus/Ansible/blob/main/Images/inNodeSystem_copy.PNG)

### Then Type
```bash
sudo systemctl restart sshd
```
# Now Go to Master Machine Type This Command
```bash
ansible all -m ping
```
