# Azure_Cloud_Security
Cloud Infrastructure.
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

 Project 1 Red Team Network Diagram(diagrams/Red Team Network Diagram.jpg)

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
- What aspect of security do load balancers protect? 
     prevent overloading servers, optimizes productivity and maximum uptime.

- What is the advantage of a jump box?
	Jump box is very highly secured computers and very less chances of hackers/malware infection.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
- What does Filebeat watch for?
	Filebeat monitors the log files and forwards to Elasticsearch/Logstash for indexing.

- What does Metricbeat record?
	Metricbeats records metrics/statistics data and transport to the output that you set up thru Elasticsearch/Logstash

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| ELK-VM   | Server   | 10.1.0.4   | Linux            |
| Web-1    | Server   | 10.0.0.6   | Linux            |
| Web-2    | Server   | 10.0.0.7   | Linux            |
| Web-3    | Server   | 10.0.0.9   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- LocalHost IP Address

Machines within the network can only be accessed by Jump-Box_Provisioner.
- Which machine did you allow to access your ELK VM? 
	Jump-Box-Provisioner
- What was its IP address?
	10.0.0.4 (private)


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

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?
	-The main advantge is YAML Playbooks. These Playbooks are used for automation configuration.
	-It is also useful to automate complex multi-tier software application environments.

The playbook implements the following tasks:
-  In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
	- SSH into Jump-Box_Provisioner  (ssh azadmin@IPAddress)
	- Start Ansible Docker  (sudo docker start <Name>) then (sudo docker attach <Name>)
	- Changed path to /etc/ansible/files directory and created ELK playbook (ELK_Playbook.yml)
	- Ran the ELK_Playbook.yml in the same direcrory.(ansible-playbook ELK_Playbook.yml)
	- Finally, SSH into the ELK-VM to verify the server is up and running.
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
	Project 1 Red Team Network Diagram(diagrams/Red Team Network Diagram.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- List the IP addresses of the machines you are monitoring
	Web-1 10.0.0.6
	Web-2 10.0.0.7
	Web-3 10.0.0.9


- We have installed the following Beats on these machines:
	Filebeat 
	Metricbeat

These Beats allow us to collect the following information from each machine:
- In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
	- Filebeat is used to collect log files from specific files on remote machines.
	- Filebeats examples are file generated by Apache, Microsoft Azure Tools, Nginx web server and MySQL databases
	- Metricbeat collect machine metric
	- Metricbeat examples are CPU Usage/Uptime.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-configuration.yml file to /etc/ansible/roles/files.
- Update the filebeat-configuration.yml file to include the ELK private IP in lines 1106 and 1806.
- Run the playbook, and navigate to (ELK-VM public IP) to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
copy the metricbeat-configuration.yml file to /etc/ansible/roles/files.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

Update the metricbeat-configuration.yml file to include the ELK private IP in lines 62 ans 96.
- _Which URL do you navigate to in order to check that the ELK server is running?
Run the playbook and naviage to (ELK-VM public IP) to check that the installation working as expected.

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
