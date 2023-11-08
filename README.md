
# Introduction to Ansible Workshop

**What is Ansible?**
Ansible is an open-source automation tool that simplifies and accelerates IT tasks, making system administration, configuration management, and application deployment easier and more efficient. In this workshop, you will learn the fundamentals of Ansible and how to leverage it for automating various tasks in your IT environment.

<center>
  <img src="https://sloopstash.com/assets/image/training/ansible/icon.svg"
style="width: 300px"
    />
</center>

In our Ansible workshop, we'll create a simulated network environment with virtual machines. This hands-on approach will help us gain practical experience, tackle real-world scenarios, and develop valuable automation skills that apply to IT tasks in complex settings. The architecture of our mock infrastructure is as follows:



**Workshop Goals:**
- Gain a foundational understanding of Ansible and its core concepts.
- Learn how to write Ansible playbooks to automate tasks and configurations.
- Understand how to manage systems, applications, and infrastructure with Ansible.

In our Ansible workshop, we'll create a simulated network environment with virtual machines. This hands-on approach will help us gain practical experience, tackle real-world scenarios, and develop valuable automation skills that apply to IT tasks in complex settings. The infrastructure we will be working with in this workshop.

![Infrastructure architecture](https://raw.githubusercontent.com/BenkamaSalma/DevOpsProject/main/images/Infrastructure.png)

We will have two Linux machines each having its own responsibility (backend server and database) connected to an Ansible control node in our use case, your machine. We will explain how to setup this Architecture in the following sections.

---

## Infrastructure implementation
In this section we will take you over the steps to create the architecture mentioned above in a virtual Environment.

### Here's a step-by-step installation guide for setting up two Ubuntu virtual machines (VMs) in VMware Workstation:
### Step 1: Prepare Your Environment
 1. Download VMware Workstation:
 2. Download Ubuntu ISO:
 * Download the Ubuntu Desktop ISO image from the official Ubuntu website (https://ubuntu.com/download/desktop).![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/cd24797e-689c-4153-aee2-4d46e91e6091)


### Step 2: Create and Install the First Ubuntu VM
 1. Open VMware Workstation:
 * Launch VMware Workstation.

 2. Create a New Virtual Machine:
 ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/5d3486d4-8a71-4555-b8d8-196288a9337d)

 3. New Virtual Machine Wizard
 * Choose "Typical" and click "Next."
![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/72de9028-ac24-4d46-aa05-b5ebf98f4817)

 4. Select a Disk:
 * Choose "Installer disc image file (iso)" and browse to the Ubuntu ISO file you downloaded.
 * Click "Next."
![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/15154b79-5da8-40b4-bf61-84f1f403474e)

 5. Name and Location:
 * Choose a name for your VM (e.g., "Ubuntu VM1").
 * Select the location to store the VM files.
 * Click "Next."
![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/d4f0c431-6574-48cd-9d1a-ccd322a64b81)
![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/d4229137-e471-4bb5-b917-db50c8d257fc)
 ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/55d5e583-e697-4c57-8a38-2f89e10e16d9)

 6. Ready to Create Virtual Machine:
 * Review the settings and click "Finish."
 ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/0985258a-346f-4b39-97c0-721c9653c77a)
###
 7. Ready to Create Virtual Machine:
 * If you're finding trouble powering your machine try change this parameter to False in the Ubuntu 64-bit.vmx file
![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/0a1f553b-b7fc-416f-ad85-bf276db2a7bb)

 8. Setting Up the OS:
 ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/b7664fac-0b0b-44dd-b239-2174a25c150b)
![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/7248089f-37c5-4d8e-8125-143a76ad2d20)

 9. Your Machine is ready for use:
 ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/052c5fb6-3816-4e03-a4f5-b419b4659af6)

### Step 3: Create and Install the Second Ubuntu VM
 Repeat the steps from "Step 2" to create and install the second Ubuntu VM. Make sure to give it a different name (e.g., "Ubuntu VM2") and specify a different IP address during installation.

### Step 4: Set Up IP Addresses
 1. Open a Terminal:
 * Open a terminal on the Ubuntu virtual machine for which you want to set up the IP address.
 2. List Network Connections:
 * Use the following command to list your network connections to find the name of your network interface (e.g., ens33 or eth0):
 `ip address show`
 ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/a35c3be8-6f5b-4811-bce2-eaea8b73d9c8)
 * Note down the connection name (e.g., Wired connection 1) and your network interface name (e.g., ens33).
 3. Set a Static IP Address:
 * Use the following command to configure a static IP address for the network interface. Replace <connection-name>, <interface-name>, <IP-Address>, <Subnet-Mask>, and <Gateway-IP> with your specific values:
 `sudo nmcli connection add con-name <connection-name> type ethernet ifname <interface-name> ipv4.addresses <IP-Address>/<Subnet

-Mask> ipv4.method manual`
 ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/551f9478-5f66-419e-8d59-5343131767d2)
* This command creates a new network connection named "eth0" (you can change it to your preferred connection name), assigns the provided IP address (in this example, 172.25.1.4) with a subnet mask of /24 to the specified interface (ens33).
 4. Activate the Connection:
* To apply the changes, activate the newly created network connection:
`sudo nmcli connection up <connection-name>`
 ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/07569696-f605-4eec-be87-82f67f805f21)
 * Repeat these steps for your other Ubuntu virtual machine with a different IP address. After completing these steps, you will have set up static IP addresses for your virtual machines using the nmcli command.

### Step 5: Test Connectivity
 1. Ping Between VMs:
 Open terminals in both VMs and test connectivity between them by pinging each other's IP addresses.
 * From VM1: ping IP_of_VM2
 ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/d1856802-17f6-42b9-bc5b-17b93ffb8eb2)
 * From VM2: ping IP_of_VM1
 ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/3c494165-11d4-46b4-a18d-30f161cf078d)
 2. Virtual Network Editor:
 * This is How our Virtual Network Editor looks like for VM: SalmaBen
 As you can see, we added a Custom Network for our host machine in order to connect them. You can find your machine's IP address by running `ipconfig` in the host's terminal.
![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/a24d2ca5-71df-4f0b-8945-9bdb95f52a04)
 ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/3cc64ac9-cee7-4e0e-95d2-c9991ee278b6)
 * Nat Configuration for Network Editor:
Check Nat settings by adding Gateway IP and add a host port in order to connect the host machine and the virtual one successfully.
 ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/b326f010-791f-4a21-bdc0-9048a8bbfa24)
 3. Ping Between VMs:
 * Ping from the host machine:
 ![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/16f6a201-89ff-4a86-a1c2-aea87fc45e9b)
 * Ping from the virtual machine:
![image](https://github.com/BenkamaSalma/DevOpsProject/assets/91811131/b2b1e8d4-5c83-45bf-907c-661c7fd2b24d)
 
 With this guide, you should have successfully set up two Ubuntu virtual machines in VMware Workstation, configured their IP addresses, and tested their connectivity. Remember to adjust the network settings and IP addresses as needed for your specific use case.

--- 

## Ansible Setup

---

##  Your First Ansible playbook
After successfully installing ansible and enabling ssh in host machines we can now test our setup by running this playbook.
```yml
 - name: Ping hosts
  hosts: servers
  tasks:
   - name: ping the hosts
     ping:
```
In ansible a playbook is YAML file describing a set of instruction to be ran on host machines in our case the task we are running is ping. The hosts designated in the code above as servers should be provided in inventory file which is a file containing a list of our host machines following the ini format. it should look something like this.
```ini
[servers]
webapp ansible_host={host ip} ansible_user={host user} ansible_password={host password}

database ansible_host={host ip} ansible_user={host user} ansible_password={host password}
```
we can run our playbook using this command :
```bash 
ansible-playbook -i inventory.ini playbook.yml 
```

the result should look like this 

![enter image description here](https://github.com/BenkamaSalma/DevOpsProject/blob/main/images/ping_success.png?raw=true)

## A more elaborate use case

Now that we made sure ansible is up and running we can move on to configuring our two virtual machines using ansible.

### Database

Firstly we will configure an sql database using ansible to showcase how easy it is once you have written a playbook, before we do that let's tweak the inventory to indicate a difference between the hosts.

```ini
[webservers]
webapp ansible_host={your host's ip address} ansible_user={your password} ansible_password={your password}
[databases]
database ansible_host={your host's ip address} ansible_user={your password} ansible_password={your password}
```
Here's what each part of the inventory file describes:

**[webservers] and [databases]:** These are group names that group hosts into categories. In this case, "webservers" and "databases" are used to group hosts that serve as web servers and database servers, respectively.

**webapp and database:** These are the host names or aliases within their respective groups. They are used as identifiers for the hosts within the group.

**ansible_host:** This is the IP address of the host that Ansible will connect to for configuration management. Each host in the "webservers" and "databases" groups is associated with a specific IP address.

**ansible_user:** This is the SSH or remote login username that Ansible will use when connecting to the host. It should be a valid username with the necessary permissions to perform tasks on the host.

**ansible_password:** This is the password required to authenticate with the host. Note that specifying the password in the inventory file is generally not recommended for security reasons. It's better to use SSH key authentication or Ansible Vault for secure password management.

Now we can write a playbook that only runs on hosts described as databases
```yml
- name: setup Mysql with db and remote login
  become: yes
  hosts: databases
  tasks:
    - name: Installing Mysql  and dependencies
      package:
         name: "{{item}}"
         state: present
         update_cache: yes
      loop:
        - mysql-server
        - mysql-client
        - python3-mysqldb
        - libmysqlclient-dev
      become: yes

    - name: start and enable mysql service
      service:
         name: mysql
         state: started
         enabled: yes

    - name: creating mysql user (medium_post)
      mysql_user:
         name: "devops"
         password: "devops123"
         priv: '*.*:ALL'
         host: '%'
         state: present

    - name: creating medium_db
      mysql_db:
         name: "devops"
         state: present

    - name: Enable remote login to mysql
      lineinfile:
         path: /etc/mysql/mysql.conf.d/mysqld.cnf
         regexp: '^bind-address'
         line: 'bind-address = 0.0.0.0'
         backup: yes
      notify:
        - Restart mysql

  handlers:
    - name: Restart mysql
      service:
        name: mysql
        state: restarted

```

This playbook automates the setup of MySQL, including user and database creation, as well as enabling remote access to the MySQL server. It's an example of infrastructure as code using Ansible, allowing you to consistently configure MySQL on multiple hosts.

We can run this playbook using this command
```bash
ansible-playbook -i inventory.ini db.yml 
```
If you have set the ssh password to be the same as the root password this should work just fine however if you encounter a missing sudo password error add -K to the end of the command and ansible will prompt you to give the host's privilege escalation password (root password).

We can verify the database is up and running logging into the machine using ssh and running the following command:
```bash
systemctl status mysql.service
```
If the service is running correctly you should see the following output: 
![service status](https://github.com/BenkamaSalma/DevOpsProject/blob/main/images/status.png?raw=true)

You can also connect to mysql using the user created in the playbook by running this command.
![enter image description here](https://github.com/BenkamaSalma/DevOpsProject/blob/main/images/db.png?raw=true)

Using this playbook you can set multiple databases in multiple servers using a single command.

### Webserver

In this section, we will use Ansible modules to clone a Git repository containing a web application, build a Docker image, and run the webserver. But before we dive into the practical steps, let's understand what Ansible modules are and how they play a crucial role in automating tasks within Ansible.

**What Are Ansible Modules?**

Ansible modules are small, self-contained units of code that Ansible uses to perform specific tasks or actions on remote hosts. They are like building blocks that allow Ansible to interact with and manage various aspects of a system or application. Modules simplify automation by encapsulating the logic needed to perform tasks such as installing software, configuring settings, copying files, managing users, and more.

Each module is designed for a particular task, making it easy to perform complex operations without having to write custom scripts or commands. Ansible comes with a vast library of built-in modules, covering a wide range of tasks, and you can also create custom modules when needed.

**How Modules Work:**

When you define tasks in an Ansible playbook, you specify which module to use for each task, provide any necessary parameters, and describe the desired state of the system. Ansible takes care of executing the task on the remote host by invoking the relevant module with the provided parameters. The module performs the task and returns the results to Ansible for reporting.

For example, in our case, we will use modules like `git`, `docker_image`, and `docker_container` to:

1. Use the `git` module to clone the web application's source code from a Git repository.
2. Use the `docker_image` module to build a Docker image from the application code.
3. Use the `docker_container` module to run the webserver within a Docker container.

By leveraging these modules, we can automate the entire process, ensuring consistency and repeatability across multiple hosts.

In the upcoming steps, we'll put these concepts into practice and demonstrate how Ansible modules simplify the deployment of a web application in a Docker container.




