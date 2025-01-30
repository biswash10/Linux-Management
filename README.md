# Linux-Management
# 2025-01-19
- Biswash Pokhrel, amk1004574@student.hamk.fi

# Task
How to create a virtual machine to used Azure Platform for Linux Management Course.

- Step 1: At first, I create a Azure account from portal.azure.com for myself using my university email. 


![Azure View after login ] 
![alt text](<Screenshot 2025-01-20 220903.png>)

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

![Successfully done in Terminal ]!![alt text](<Screenshot (12).png>)




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
![alt text](<Screenshot (13).png>)
