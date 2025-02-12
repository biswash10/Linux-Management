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