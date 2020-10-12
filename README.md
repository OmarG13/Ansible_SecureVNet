# Ansible_SecureVNet
Ansible deployed secure Virtual Network

The files in this repository were used to configure the network depicted below.

<img src="https://github.com/OmarG13/Ansible_SecureVNet_with_ElkStack/blob/main/Diagrams/Elk%20integration%20into%20Secure%20VM%20Diagram.png?raw=true">

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the 3-elk-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting in-bound access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logfiles and system files as well as monitor system CPU, memory and load.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.7   | Linux            |
| Web-1    | DVWA     | 10.0.0.5   | Linux            |  
| Web-2    | DVWA     | 10.0.0.9   | Linux            |
| Web-3    | DVWA     | 10.0.0.4   | Linux            |
| Elk      | Monitor  | 10.1.0.4   | Linux            |

In addition to the above, Azure has provisioned a load balancer in front of all machines except for the jump box. The load balancer has 1 availability zone for Web-1, Web-2 and Web-3.

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 194.***.***.***

Machines within the network, including the Elk stack machine, can only be accessed by the Jump Box on 10.0.0.7

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 194.***.***.***      |
| Web-1    | No                  | 10.0.0.1-254         |
| Web-2    | No                  | 10.0.0.1-254         |
| Web-3    | No                  | 10.0.0.1-254         |
| Elk      | No                  | 10.0.0.1-254         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it reduces human error, is reusable, easy, quick and efficient. 

The playbook implements the following tasks:
- Downloads and installs Docker
- Downloads and installs Python
- Downloads and installs Python Docker Module
- Increases and uses more virtual memory
- Downloads and launches Docker Elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img src="https://github.com/OmarG13/Ansible_SecureVNet_with_ElkStack/blob/main/Diagrams/Elk%20Docker.PNG?raw=true">

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.9
- Web-3 10.0.0.4

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat
- Auditbeat

These Beats allow us to collect the following information from each machine:
- Filebeat: Collects log file events and data and allows them to be indexed and displayed in various ways. Ex:SSH logins.
- Metricbeat: Monitors performance of the machines, displaying system CPU, memory and load. Ex: File storage overview.
- Auditbeat: Collects and displays audit activities of users and processes. Ex: Package count and changes.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned (if not, please look into the Linux folder and read the file install Ansible): 

SSH into the control node (Jump Box) and follow the steps below:
- Copy the contents of the yaml playbook elk-playbook.yml file to the Ansible control node on Jump Box.
- Update the yaml playbook elk-playbook.yml file to include the correct target machines.
- Run the playbook, and navigate to http://{Elk virtual machine public IP}:5601 to check that the installation worked as expected.

Use the below commands:
```
ssh username@{Jump Box public IP}
sudo docker container list -a
sudo docker start {ansible container ID}
sudo docker attach {ansible container ID}
cd /etc/ansible/
nano elkplaybook_{name}.yml
```
* copy/paste the contents of elk-playbook.yml into the newly created elkplaybook_{name}.yml
* update the "hosts:" section of elkplaybook_{name}.yml to indicate the target machine(s)
* save and close the yaml file
```
ansible-playbook elkplaybook.yml
```
