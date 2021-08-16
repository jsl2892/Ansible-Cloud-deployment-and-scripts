## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![uclacyberhw12diagram](https://user-images.githubusercontent.com/83263482/129510166-62518f2d-e3f0-4454-898b-87a98ea2dd23.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

 [Ansibleymlscripts.docx](https://github.com/jsl2892/UCLA-cybersecurity-bootcamp-work/files/6989733/Ansibleymlscripts.docx)



This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.The load balancer ensures that work to process incoming traffic will be shared by both vulnerable web servers. Access controls will ensure that only authorized users — namely, ourselves — will be able to connect in the first place.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the VMs on the network and system metrics.
Filebeat detects changes to the filesystem. 
Metricbeat records changes in system metrics.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| DVWA 1   |Web Server| 10.0.0.5   | Linux            |
| DVWA 2   |Web Server| 10.0.0.6   | Linux            |
| ELK      |Monitoring| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
172.90.42.45

Machines within the network can only be accessed by each other.
The DVWA 1 and DVWA 2 VMs send traffic to the ELK server with IP 10.0.0.5 and 10.0.0.6 respectively.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 |     172.90.42.45     |
| ELK      | no                  |     10.0.0.1-254     |
| DVWA 1   | no                  |     10.0.0.1-254     |
| DVWA 2   | no                  |     10.0.0.1-254     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
The primary benefit of Ansible is it allows IT administrators to automate away the drudgery from their daily tasks. That frees them to focus on efforts that help deliver more value to the business by spending time on more important tasks

The playbook implements the following tasks:
- Install Docker
- Increase memory
- Install python3-pip
- Download and launch a docker elk container with ports at 5601,9200,5044.
- enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![configureelkvmwithdockerpic](https://user-images.githubusercontent.com/83263482/129511740-3d412150-4fd1-406d-ab23-753ddb8468eb.PNG)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
This ELK server is configured to monitor the DVWA 1 and DVWA 2 VMs, at 10.0.0.5 and 10.0.0.6, respectively.

We have installed the following Beats on these machines:
Filebeat and Metricbeat.

These Beats allow us to collect the following information from each machine:
Filebeat: Filebeat detects changes to the filesystem. Specifically, we use it to collect Apache logs.
Metricbeat: Metricbeat detects changes in system metrics, such as CPU usage. We use it to detect SSH login attempts, failed sudo escalations, and CPU/RAM statistics.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbooks file to ansible control node.
- Update the hosts file to include webservers and ELK
- Run the playbook, and navigate to http://10.1.0.4:5601  to check that the installation worked as expected.

- _Which file is the playbook? Where do you copy it? ansible-playbook
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?  hosts file and ansible-playbook install_filebeat.yml webservers
- _Which URL do you navigate to in order to check that the ELK server is running? curl http://10.0.0.8:5601

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._



