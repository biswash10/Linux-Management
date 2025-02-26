# Linux-Management
# 2025-01-19
- Biswash Pokhrel, amk1004574@student.hamk.fi

# Task
How to create a virtual machine to used Azure Platform for Linux Management Course.

- Step 1: At first, I create a Azure account from portal.azure.com for myself using my university email. 


![Azure View after login ] 
![alt text](Pictures/Screenshot%202025-01-20%20220903.png)

- Step 2: I created a new resource group  and new virtual machine in Azure portal.

- Step 3: I selected North Europe as a Region and Ubuntu Server 24.04 LTS - x64 Gen2 as the operating system. 

- Step 4: I selected the virtual machine size as Standard_B2ls_v2- 2 vCPUs, 4 GiB Memory ($33.29/month).

- Step 5: I selected the network configuration as Public IP address and Network interface and created a new Username (ares).

- Step 6: I seleceted OS disk type as Standard SSD and Storage type as Locally-redundant storage.

- Step 7: I selected the public IP address as Static and created a new public IP address as lab-robotics-ip.

- Step 8: I selected inbound ports as (Http(80), HTTPS(443), SSH(22))

- Step 9: I selected the Enable auto-shutdown and set the auto-shutdown time as 2:00 AM and Select the time Zone as (UTC + 2:00) Helsinki

- Step 10: I reviewed the settings and created the virtual machine.

After creating the virtual machine, I go to lab-robotics-ip and select setting(Configuration) than type ares-lab-robotics as DNS name lable and save it.

- Step 11: After that, I select lab-robotics and select connect and select Native SSH and copy the path that I downloaded the key.pam file.


- Step 12: I open the terminal and paste the URL given in SSH to VM with specified private key.

![Successfully done in Terminal ]!![alt text](Pictures/Screenshot%20(12).png)




# 2025/01/30

#  User management and file system access



1. Creating Users Tupu (Using) To create the user tupu, use the following command:
```
 sudo adduser tupu
 ```

This will:

Create a new user tupu.

Automatically create the home directory /home/tupu.

Set the default shell to /bin/bash.

Prompt for password creation and additional user details.

Tupu (Using) To create the user lupu, use the following command:
```
  sudo useradd -m -d /home/lupu -s /bin/bash -G lupu lupu
```

This will:

Create the user lupu

Set the home directory to /home/lupu

Assign the default shell /bin/bash

Add lupu to the lupu group

Set a password for lupu:
```
    sudo passwd lupu
 ```
Hupu (System User) To create a system user hupu with restricted login, use:
```
sudo useradd --system --shell /bin/false hupu
```
This ensures that hupu cannot log in interactively.

2. Granting Sudo Privilege Method 1: Using (Recommended) Edit the sudoers file safely:
```
 sudo visudo 
 ```
Add the following lines at the end:
```
    tupu ALL=(ALL:ALL) ALL
    lupu ALL=(ALL:ALL) ALL
```
Save and exit.

Method 2: Adding Users to the Group Alternatively, run:
```
    sudo usermod -aG sudo tupu
    sudo usermod -aG sudo lupu
```
3. Setting Up Shared directory sudo mkdir -p /opt/projekti sudo groupadd projekti sudo usermod -aG projekti tupu sudo usermod -aG projekti lupu sudo chown -R :projekti /opt/projekti sudo chmod 2770 /opt/projekti

4. Verification Check user groups:
```
 groups tupu
 groups lupu
```
Check directory permissions:
```
    ls -ld /opt/projekti
```

## Output
![alt text](Pictures/Screenshot%20(13).png)




# Linux Assignment : 6 Managing Packages with APT

Date: 2025-02-12
Author: Biswash Pokhrel (amk1004574@student.hamk.fi)

## Objective
By completing this assignment, we will:

- Learn to install, update, remove, and search for software using the Advanced
Package Tool (APT).

- Develop an understanding of repository management and dependency resolution.

- Gain practical experience in troubleshooting package installation issues.


# Part 1: Understanding APT & System Updates

### 1. Check your system’s APT version
Run the following command to display the installed APT version:

```bash
apt --version
```
![alt text](Pictures/Screenshot%202025-02-12%20220928.png)

### 2. Update the package list
```bash
sudo apt update
```
### Why is this important?
- The sudo apt update command refreshes the local package index with the latest changes from the repositories. This ensures that the system knows about the newest versions of packages and their dependencies. Without this step, the system might not be aware of available updates or new packages.

### 3. Upgrade installed packages
### Command:
```bash
sudo apt upgrade -y
```
### What is the difference between update and upgrade?


| Update| Upgrade | 
| ---| --- | 
| Update refreshes the list of available packages and their versions.| Upgrade installs newer versions of the packages currently installed on the system. |

### 4. View pending updates(if any)
``` bash
sudo apt list --upgradable
```
![alt text](Pictures/Screenshot%202025-02-12%20223013.png)

## Part 2: Installing & Managing Packages
``` bash
apt search image editor
```
- I used Zim image editor as an example.

### 6. View package details
``` bash
apt show zim
```
![alt text](Pictures/Screenshot%202025-02-12%20223545.png)

### 7. Install a package
``` bash
sudo apt install zim -y
```
### 8. Check installed package version
``` bash 
 apt list --installed | grep zim
```
![alt text](Pictures/Screenshot%202025-02-12%20224503.png)

## Part 3: Removing & Cleaning Packages
### 9. Uninstall the package
``` bash
sudo apt remove zim -y
``` 
![alt text](Pictures/Screenshot%202025-02-12%20224903.png)

###Is the package fully removed?

- No, configuration files are still retained.

### 10. Remove configuration files as well
``` bash 
sudo apt purge zim -y
```
### What is the difference between remove and purge?
| Remove|Purge | 
| ---| --- | 
| It  removes the package but keeps configuration files.| It removes the package along with its configuration files.|

### 11. Remove package dependencies
``` bash 
sudo apt autoremove -y
```
### Why is this step important?

- This removes unused dependencies that were installed automatically but are no longer needed, freeing up disk space.

### 12. Clean up downloaded package files
``` bash 
sudo apt clean
```
### What does this command do?
- It removes cached package files (.deb files) from /var/cache/apt/archives/, freeing up disk space.

### Part 4: Managing Repositories & Troubleshooting

### 13. List all available repositories
- while running
``` bash 
sudo cat /etc/apt/sources.list
```
![alt text](Pictures/Screenshot%202025-02-12%20230156.png)

- Then i use this
``` bash
sudo cat /etc/apt/sources.list.d/ubuntu.sources
```
![alt text](Pictures/Screenshot%202025-02-12%20230430.png)

### 14. Add a new repository
``` bash
sudo add-apt-repository universe
sudo add update
```
### What types of packages are found in the universe repository?

- The universe repository contains community-maintained free and open-source software.

### 15. Simulate an installation failure and troubleshoot
``` bash
sudo apt install fakepackage
```
### What error message do you get?
- I got:  E: Unable to locate package fakepackage

![alt text](Pictures/Screenshot%202025-02-12%20230835.png)

### How would you troubleshoot this issue?
- Check if the package name is correct.
- Ensure the repository containing the package is enabled (sudo apt update).
- Search for the package using apt search fakepackage.
- If the package doesn't exist, look for alternatives or check if it's available in a PPA.

## Bonus Challenge

### 1. Use apt-mark to hold and unhold a package
``` bash 
sudo apt-mark hold tweak
```
![alt text](Pictures/Screenshot%202025-02-12%20231212.png)

### 2. Use apt-mark to unhold a package
``` bash 
sudo apt-mark unhold tweak
```
![alt text](Pictures/Screenshot%202025-02-12%20231406.png)

### Why would you want to hold a package?
- Holding a package prevents it from being automatically updated. This is useful when you want to keep a specific version of a package for compatibility or stability reasons.


# Assignment 7: Linux Virtualization

###  18.02.2025   Biswash Pokhrel  (amk1004574@student.hamk.fi)

## Part 1: Virtualization Concepts

Virtualization: A technique that allows the creation of virtual versions of physical resources like hardware, storage, and networks.

Hypervisor: A specialized software that enables the creation and management of virtual machines (VMs). Some common examples are KVM, VMware, and Hyper-V.

Virtual Machines (VMs): Fully independent emulations of physical computers, each running its own operating system.

Containers: Lightweight, self-contained environments that operate independently while sharing the host system's OS kernel. They include their own file systems and libraries.

## VMs vs Containers

- The difference between VMs and Containers in terms of Architecture, Resource Utilization and Isolation

| **Aspect**    | **VMs**                                          | **Containers**    |
|----------------------|------------------------------------------------|------------------------------|
| **Architecture**     | Requires a full OS for each instance            | Shares the host OS kernel      |
| **Resource Utilization** | Requires more resources                        | More lightweight and efficient   |
| **Isolation**        | Provides strong isolation since each VM has its own OS | Provides a lower level of isolation, as it shares the host OS kernel |

## Part 2: Multipass Implementation
### Install Multipass
```bash
sudo snap install multipass
```
![alt text](<Pictures/Screenshot 2025-02-23 112016.png>)

### Launch an instance
```bash

multipass launch --name biswash-vm
```
![alt text](<Pictures/Screenshot 2025-02-23 112448.png>)

### List all running instances
```bash
 multipass list
```
![alt text](<Pictures/Screenshot 2025-02-23 112641.png>)

### View details about an instance
```bash
multipass info biswash-vm
```
![alt text](<Pictures/Screenshot 2025-02-23 112830.png>)

### Access the shell of a running instance
```bash
multipass shell biswash-vm
```
![alt text](<Pictures/Screenshot 2025-02-23 113049.png>)

### Stop, delete and purge an instance
```bash
multipass stop biswash-vm
multipass delete biswash-vm
multipass purge
```
![alt text](<Pictures/Screenshot 2025-02-23 114044.png>)

## Learn About Cloud-Init Configuration
### Create a cloud-init.yaml file to customize an instance.

```bash
nano cloud-init.yaml
``` 
### Launch an instance with cloud-init
```bash
 multipass launch --name biswash-vm --cloud-init cloud-init.yaml
```
![alt text](<Pictures/Screenshot 2025-02-23 114946.png>)
### Create a new folder and Mount the folder inside a VM:
```bash
mkdir ~/multipass_shared
multipass mount ~/multipass_shared biswash-vm:/mnt/shared
```
![alt text](<Pictures/Screenshot 2025-02-23 115330.png>)

### create a txt file inside multipass folder to share it in VM because without creating a file I can't mount the folder.

```bash
echo "Hello, World!" > ~/multipass_shared/testfile.txt
```
![alt text](<Pictures/Screenshot 2025-02-23 115531.png>)
### Check the mounted folder inside the VM:

```bash 
multipass shell biswash-vm
ls /mnt/shared
```
![alt text](<Pictures/Screenshot 2025-02-23 115756.png>)

## Part 3: LXD Implementation

### Installation
```bash 
sudo apt update
sudo snap install lxd
```
![alt text](<Pictures/Screenshot 2025-02-23 120441.png>)

## Basic LXD command
### Create a new container ans list it
```bash
lxc launch ubuntu:24.04 biswash-container
lxc list
```
![alt text](<Pictures/Screenshot 2025-02-24 221538.png>)

### Start and stop the container
```bash
lxc start biswash-container
lxc stop biswash-container
```
![alt text](<Pictures/Screenshot 2025-02-24 221857.png>)

### Delete the container
```bash
lxc delete biswash-container
```
![alt text](<Pictures/Screenshot 2025-02-24 222151.png>)

## Part 4: Docker
### Installation
```bash
# Install Docker Engine
sudo apt update
sudo apt install docker.io

# Start and enable Docker
sudo systemctl start docker
sudo systemctl enable docker
```

### Verify the installation
```bash
docker --version
```
![alt text](<Pictures/Screenshot 2025-02-24 223244.png>)

### Basic Docker Commands
```bash
# Pull image
docker pull ubuntu:latest

# Run container
docker run -it ubuntu:latest

# List containers
docker ps

# Build from Dockerfile
docker build -t myapp .

# Stop container
docker stop container_id
```
![alt text](<Pictures/Screenshot 2025-02-26 184833.png>)

## Part 5: Snap Implementation
What are snaps?


Snaps are universal, containerized software packages that include all dependencies needed to run an application. They work across multiple Linux distributions without requiring separate packaging for each one.



What is Snapcraft?

Snapcraft is a tool developed by Canonical for building, packaging, and publishing Snap applications. It simplifies the process of creating Snaps, ensuring they work across multiple Linux distributions without dependency conflicts.

## Install Snapcraft
First, install snapcraft
```bash
sudo apt update
sudo apt install snapcraft -y
```
If you're on a non-Ubuntu system, you may need to install Snapcraft via Snap:
```bash
sudo snap install snapcraft --classic
```
### Verify Snapcraft installation
```bash
snapcraft --version
```
![alt text](<Pictures/Screenshot 2025-02-26 185906.png>)

### Create a directory for Snap project
```bash
    mkdir my-snapcraft
    cd my-snapcraft
```
### Create a simple Application Script
We'll make a simple bash script that prints "Hello, Snap!".
```bash
mkdir bin
nano bin/hello-snap
```
Add the following code to the file:
```bash
#!/bin/bash
echo "Hello, Snap!"
```
### Create a Snapcraft Configuration File
Initialize snapcraft
```bash
snapcraft init
```
Edit the snapcraft.yaml file
```bash
nano snapcraft.yaml
```
Add the following content to the file:
```bash
name: my-snapcraft
base: core22
version: "1.0"
summary: "A simple Snapcraft app"
description: "This is a simple Snap application that prints Hello, Snap!"

grade: stable
confinement: strict

apps:
  hello:
    command: bin/hello-snap

parts:
  hello:
    plugin: dump
    source: .
```
![alt text](<Pictures/Screenshot 2025-02-26 190456.png>)

### Build the Snap
<<<<<<< HEAD
```bash
snapcraft
```
### Install the Snap:
```bash
sudo snap install my-snapcraft_1.0_amd64.snap --dangerous
```
The --dangerous flag is needed because it's not for the offical Snap store.

Run the Snap:
```bash
my-snapcraft.hello
```
