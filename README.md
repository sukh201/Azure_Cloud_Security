# Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.

![Red Team Cloud Network Diagram](https://user-images.githubusercontent.com/2991161/134776756-f2b46ae7-56e8-42a2-9dba-b51f592438ba.jpg)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Project 1 Tead Team Network Diagram file may be used to install only certain pieces of it, such as Filebeat.

  - filebeat-playbook.yml
  - filebeat-configuration.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly funtional, in addition to restricting high traffic to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.

The configuration details of each machine may be found below.

| Name     | Function      | IP Address | Operating System |
|----------|---------------|------------|------------------|
| Jump Box | Gateway       | 10.0.0.4   | Linux            |
| ELK-VM   | Server-DVMA   | 10.1.0.4   | Linux            |
| Web-1    | Server-DVMA   | 10.0.0.6   | Linux            |
| Web-2    | Server-DVMA   | 10.0.0.7   | Linux            |
| Web-3    | Server-DVMA   | 10.0.0.9   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- LocalHost IP Address

Machines within the network can only be accessed by Jump-Box_Provisioner.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | LocalHost(IP Address)|
| ELK-VM * | No                  | 10.0.0.4             |
| Web-1*   | No                  | 10.0.0.4             |
| Web-2*   | No                  | 10.0.0.4             |
| Web-3*   | No                  | 10.0.0.4             |

* -- All these VMs can only be accessed from the Jump-Box_provisioner

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because mistakes can be made. A script can be modified to perfection before use.

The playbook implements the following tasks:
 - Downloads, instals and configures Docker on every VM on both networks
 - Downloads and installs DVWA, Metricbeat, and Filebeat on the web machines.
 - Downloads and installs a Docker container for ELK on the ELK server.

Steps:
 	- SSH into Jump-Box_Provisioner  (ssh azadmin@IPAddress)
	- Start Ansible Docker  (sudo docker start <Name>) then (sudo docker attach <Name>)
	- Changed path to /etc/ansible/files directory and created ELK playbook (ELK_Playbook.yml)
	- Ran the ELK_Playbook.yml in the same direcrory.(ansible-playbook ELK_Playbook.yml)
	- Finally, SSH into the ELK-VM to verify the server is up and running.
	
The following screenshot display the result of running Kibana on the ELK server
	Images/Kibana_Home.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
	Web-1 10.0.0.6
	Web-2 10.0.0.7
	Web-3 10.0.0.9

- We have installed the following Beats on these machines:
	Filebeat 
	Metricbeat

These Beats allow us to collect the following information from each machine:
	- Filebeat is used to collect log files like errors or authorization attempts from specific files on remote machines.
	- Metricbeat collect machine information like CPU usage, Network load, memory usage etc.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-configuration.yml file to /etc/ansible/roles/files.
- Update the filebeat-configuration.yml file to include the ELK private IP in lines 1106 and 1806.
- Run the playbook, and navigate to (ELK-VM public IP) to check that the installation worked as expected.

