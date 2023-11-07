
## Here's a step-by-step installation guide for setting up two Ubuntu virtual machines (VMs) in VMware Workstation:
## Step 1: Prepare Your Environment
### 1. Download VMware Workstation:
### 2. Download Ubuntu ISO:
#### * Download the Ubuntu Desktop ISO image from the official Ubuntu website (https://ubuntu.com/download/desktop).
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/cd24797e-689c-4153-aee2-4d46e91e6091)

##
## Step 2: Create and Install the First Ubuntu VM
### 1. Open VMware Workstation:
#### * Launch VMware Workstation.
###
### 2. Create a New Virtual Machine:
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/5d3486d4-8a71-4555-b8d8-196288a9337d)
###
### 3. New Virtual Machine Wizard
#### * Choose "Typical" and click "Next."
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/72de9028-ac24-4d46-aa05-b5ebf98f4817)
###
### 4. Select a Disk:
#### * Choose "Installer disc image file (iso)" and browse to the Ubuntu ISO file you downloaded.
#### * Click "Next."
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/15154b79-5da8-40b4-bf61-84f1f403474e)
###
### 5. Name and Location:
#### * Choose a name for your VM (e.g., "Ubuntu VM1").
#### * Select the location to store the VM files.
#### * Click "Next."
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/d4f0c431-6574-48cd-9d1a-ccd322a64b81)
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/d4229137-e471-4bb5-b917-db50c8d257fc)
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/55d5e583-e697-4c57-8a38-2f89e10e16d9)
###
### 6. Ready to Create Virtual Machine:
#### * Review the settings and click "Finish."
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/0985258a-346f-4b39-97c0-721c9653c77a)
###
### 7. Ready to Create Virtual Machine:
#### * If you're finding trouble powering your machine try change this parameter to False in the Ubuntu 64-bit.vmx file
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/0a1f553b-b7fc-416f-ad85-bf276db2a7bb)
###
### 8. Setting Up the OS:
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/b7664fac-0b0b-44dd-b239-2174a25c150b)
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/7248089f-37c5-4d8e-8125-143a76ad2d20)
###
### 9. Your Machine is ready for use:
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/052c5fb6-3816-4e03-a4f5-b419b4659af6)
###
## Step 3: Create and Install the Second Ubuntu VM
### Repeat the steps from "Step 2" to create and install the second Ubuntu VM. Make sure to give it a different name (e.g., "Ubuntu VM2") and specify a different IP address during installation.
##
## Step 4: Set Up IP Addresses
### 1. Open a Terminal:
#### * Open a terminal on the Ubuntu virtual machine for which you want to set up the IP address.
### 2. List Network Connections:
#### * Use the following command to list your network connections to find the name of your network interface (e.g., ens33 or eth0):
#### `ip address show`
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/a35c3be8-6f5b-4811-bce2-eaea8b73d9c8)
#### * Note down the connection name (e.g., Wired connection 1) and your network interface name (e.g., ens33).
### 3. Set a Static IP Address:
#### * Use the following command to configure a static IP address for the network interface. Replace <connection-name>, <interface-name>, <IP-Address>, <Subnet-Mask>, and <Gateway-IP> with your specific values:
#### `sudo nmcli connection add con-name <connection-name> type ethernet ifname <interface-name> ipv4.addresses <IP-Address>/<Subnet

-Mask> ipv4.method manual`
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/551f9478-5f66-419e-8d59-5343131767d2)
#### * This command creates a new network connection named "eth0" (you can change it to your preferred connection name), assigns the provided IP address (in this example, 172.25.1.4) with a subnet mask of /24 to the specified interface (ens33).
### 4. Activate the Connection:
#### * To apply the changes, activate the newly created network connection:
#### `sudo nmcli connection up <connection-name>`
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/07569696-f605-4eec-be87-82f67f805f21)
#### * Repeat these steps for your other Ubuntu virtual machine with a different IP address. After completing these steps, you will have set up static IP addresses for your virtual machines using the nmcli command.
##
## Step 5: Test Connectivity
### 1. Ping Between VMs:
#### Open terminals in both VMs and test connectivity between them by pinging each other's IP addresses.
#### * From VM1: ping IP_of_VM2
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/d1856802-17f6-42b9-bc5b-17b93ffb8eb2)
#### * From VM2: ping IP_of_VM1
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/3c494165-11d4-46b4-a18d-30f161cf078d)
### 2. Virtual Network Editor:
#### * This is How our Virtual Network Editor looks like for VM: SalmaBen
#### As you can see, we added a Custom Network for our host machine in order to connect them. You can find your machine's IP address by running `ipconfig` in the host's terminal.
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/a24d2ca5-71df-4f0b-8945-9bdb95f52a04)
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/3cc64ac9-cee7-4e0e-95d2-c9991ee278b6)
#### * Nat Configuration for Network Editor:
#### Check Nat settings by adding Gateway IP and add a host port in order to connect the host machine and the virtual one successfully.
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/b326f010-791f-4a21-bdc0-9048a8bbfa24)
### 3. Ping Between VMs:
#### * Ping from the host machine:
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/16f6a201-89ff-4a86-a1c2-aea87fc45e9b)
#### * Ping from the virtual machine:
#### ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/b2b1e8d4-5c83-45bf-907c-661c7fd2b24d)
### With this guide, you should have successfully set up two Ubuntu virtual machines in VMware Workstation, configured their IP addresses, and tested their connectivity. Remember to adjust the network settings and IP addresses as needed for your specific use case.
