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
> **Note**
> When we install Ansible On Ubuntu, it does not have cfg files. That's why we are adding this cnf :point_left:
1. Write [defaults]
2. Write inventory = /etc/ansible/hosts
3. Write sudo_user = root
4. Write host_key_checking = False
```bash
[defaults]
inventory = /etc/ansible/hosts
sudo_user = root
host_key_checking = False
```

![Example2](https://github.com/ritikvirus/Ansible/blob/main/Images/ubuntu/ansible_configuration.PNG)

### Now Set Group And Client Node IPs
```bash
sudo vim /etc/ansible/hosts
```
Make Group **[groupname]**  
Press Enter Give Client Node IPs  

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
**Copy SSH KEY From Master Node And Past Client Nodes**  
![Example6](https://github.com/ritikvirus/Ansible/blob/main/Images/copyMaster_key.PNG)
# In All Client Nodes Use These Commands
### Type These Commands in Client Nodes 
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
***Past Copied SSH KEY From Master Node Past in Client Node***  
Go to last line then press enter then past your copied master system ssh Key
![Example7](https://github.com/ritikvirus/Ansible/blob/main/Images/inNodeSystem_copy.PNG)

### Then Type
```bash
sudo systemctl restart sshd
```
# Now Go to Master Machine (Master Node) And Type This Command
```bash
ansible all -m ping
```
![Example](https://github.com/ritikvirus/Ansible/blob/main/Images/ubuntu/final.PNG)

# Simple Ansible Playbook: Install Nginx Server on Client Node with Congratulatory Message
```bash
sudo nano playbook-name.yml
```
## Please Paste This Code In Your playbook-name.yml File
```bash
---
- name: Install and configure Nginx
  become: true
  hosts: all

  tasks:
    - name: Check if Nginx is installed
      stat:
        path: /usr/sbin/nginx
      register: nginx_installed

    - name: Install Nginx if not present
      apt:
        name: nginx
        state: present
      when: not nginx_installed.stat.exists
      register: nginx_install

    - name: Overwrite Nginx default index file
      copy:
        content: "Congrats! Your Ansible playbook is working fine."
        dest: /var/www/html/index.html
        owner: www-data
        group: www-data
        mode: '0644'
      notify:
        - restart nginx

  handlers:
    - name: restart nginx
      service:
        name: nginx
        state: restarted

```
# Run This Playbook In Your Master Node
```bash
ansible-playbook playbook-name.yml
```
