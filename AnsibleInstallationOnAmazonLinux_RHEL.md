# Ansible Installation On AWS Amazon Linux

Ansible is an open source tool that you can use to automate your AWS deployments. You can use it to define, deploy, and manage applications and services using automation playbooks. These playbooks enable you to define configurations once and deploy those configurations consistently across environments. Safe automation.
## [Follow Video Tutorial](#)

## Prerequisites
1.An AWS EC2 Instance (AmazonLinux/Centos/Recommend Amazon Linux)
2. make sure your all instance in same users login (Master) and (Node) Like ec2-user to ec2-user

## Installation

Run 
This Command
```bash
sudo yum update -y
```
```bash
sudo yum upgrade -y
```
```bash
sudo amazon-linux-extras install ansible2 -y
```
If using RHEL
```bash
sudo yum install ansible
````
And Vim Replace vi only
#### Check Ansible version And Configuration Path
![Example](https://github.com/ritikvirus/Ansible/blob/main/Images/ansible_conf_path.PNG)
## Now Open Ansible Configuration File
```bash
sudo vim /etc/ansible/ansible.cfg
```
1. Uncomment inventory = /etc/ansible/hosts
2. Uncomment sudo_user = root
3. host_key_checking = False

![Example2](https://github.com/ritikvirus/Ansible/blob/main/Images/ansible_confuncomment1.PNG)
![Example3](https://github.com/ritikvirus/Ansible/blob/main/Images/ansible_conf4.PNG)

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
![Example6](https://github.com/ritikvirus/Ansible/blob/main/Images/copyMaster_key.PNG)
**Copy SSH KEY From Master And Past Nodes**  

# All Nodes System Use These Steps
### Type These Commands in Nodes System
```bash
sudo yum update -y
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
![Example6](https://github.com/ritikvirus/Ansible/blob/main/Images/copy_in_node_auth_key.PNG)

### Then Type
```bash
sudo systemctl restart sshd
```
# Now Go to Master Machine Type This Command
```bash
ansible all -m ping
```
![example](https://github.com/ritikvirus/Ansible/blob/main/Images/ubuntu/final.PNG)
