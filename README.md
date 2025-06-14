### README Ansible Lab Project Setup

1. Control and Managed Nodes Overview

1.1 control-node: The device on which Ansible is installed and controls the rest.

1.2 node1 and node2: The devices on which the Playbooks are applied.

### 2. Installing Ansible on Windows
 
To install Ansible on Windows, follow one of the recommended methods below. Ansible doesn't run natively on Windows, so you'll need to use WSL (Windows Subsystem for Linux) or a virtual machine.

Note: Ansible cannot be installed directly on native Windows because it's Linux-based and depends on SSH.

Command:
\$ wsl --install

### 3. Setup Methods

### 3.1 Option 1: Using Vagrant (Fast Automated Setup)
You can build the 3 VMs with a single command. Each VM will be ready with a name and a specific role.

### Link Video >>>>>>  Uploading Multi-Node Configuration Management Lab with Vagrant and Virtualization.mp4…

### 3.2 Option 2: Manual Setup with VMware
You need to install Ubuntu three times and manually set up (Ansible + SSH).

### 4. Tools Required

5. VirtualBox

6. Vagrant

7. Customize Ubuntu WSL Terminal Prompt

### 5.1 Step 1: Switch to Root User
\$ sudo passwd root
\$ su -

### 5.2 Step 2: Customize the Prompt (PS1)
Edit the /root/.bashrc file:
\$ nano /root/.bashrc

Add this line at the end:
PS1='\[\u\@control-node \W]# '

Apply changes:
\$ source \~/.bashrc

Result:
\[root\@control-node \~]#

### 6. Install Ansible on Ubuntu/WSL

### 6.1 Step 1:
\$ sudo apt update && sudo apt upgrade -y

### 6.2 Step 2:
\$ sudo apt install software-properties-common -y
\$ sudo add-apt-repository --yes --update ppa\:ansible/ansible
\$ sudo apt install ansible -y

### 6.3 Step 3: Verify Installation
\$ ansible --version

### 7. Connectivity Fix (If No Internet)
   \$ nano /etc/resolv.conf

Add:
nameserver 8.8.8.8
nameserver 8.8.4.4

Then:
\$ systemctl restart NetworkManager
\$ sudo ufw status
\$ sudo ufw disable

### 8. Enable SSH for Access
   \$ sudo apt update
   \$ sudo apt install openssh-server -y
   \$ sudo systemctl enable ssh
   \$ sudo systemctl start ssh

SSH into any VM:
\$ ssh username@<vm-ip>

### 9. Step-by-Step: Ansible Lab Setup on Ubuntu VM

### 9.1 Step 1:
\$ mkdir ansible-lab && cd ansible-lab

### 9.2 Step 2: Create Vagrantfile with VM IPs, hostnames, and roles.

### 9.3 Step 3:
\$ vagrant up

### 9.4 Step 4: Access VMs
\$ vagrant ssh control-node
\$ vagrant ssh node1
\$ vagrant ssh node2

### 9.5 Step 5: Install Ansible
\$ sudo apt update
\$ sudo apt install ansible -y

### 10. Vagrant and VirtualBox Installation

VirtualBox: Download from [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)
Vagrant: Download from [https://developer.hashicorp.com/vagrant/downloads](https://developer.hashicorp.com/vagrant/downloads)

### Verify:
\$ vagrant --version

### 11. Create a Vagrant Project with 3 VMs
    \$ mkdir vagrant-lab
    \$ cd vagrant-lab
    \$ vagrant init


### Launch:
\$ vagrant up

### Access VMs:
\$ vagrant ssh control-node

### 12. Hostname and Hosts Setup
    Inside each VM:
    \$ sudo hostnamectl set-hostname <hostname>

On control-node:
\$ sudo nano /etc/hosts

### Add:
192.168.56.10 control control-node
192.168.56.11 node1
192.168.56.12 node2

### 13. Create ansible User on All Nodes
    \$ sudo useradd ansible
    \$ sudo passwd ansible


### 14. Configure SSH from control-node
    Switch to ansible:
    \$ su - ansible
    \$ ssh-keygen

### Copy key to nodes:
\$ ssh-copy-id ansible\@node1
\$ ssh-copy-id ansible\@node2

### 15. Install Ansible on control-node
    \$ sudo apt update
    \$ sudo apt install ansible -y

### 16. Important Notes

* Tools like Docker, WSL, or Hyper-V may create conflicting virtual networks.
* VirtualBox is simpler and recommended over VMware for Vagrant.

### 17. Switch Between Providers (VirtualBox vs VMware)
    Specify in Vagrantfile:
    config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    end

config.vm.provider "vmware\_desktop" do |vmw|
vmw\.gui = true
end

### Run with:
\$ vagrant up --provider=virtualbox
or
\$ vagrant up --provider=vmware\_desktop


 ### Screenshoots

 ### Control-Node 
 
 ### 0.1 ![Screenshot (72)](https://github.com/user-attachments/assets/ece90c8e-fc60-438e-9486-a6dc477ca389)

 ### Node1 (Server 1)
 
 ### 1- ![Screenshot (74)](https://github.com/user-attachments/assets/cf46844d-3662-45e7-bffe-90e24cc5b130)

 ### Node2 (Server 2)

 ### 2-3 ![Screenshot (69)](https://github.com/user-attachments/assets/d882ef66-fe5a-4145-acb6-10d907c92903)


