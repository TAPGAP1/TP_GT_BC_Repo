# TP_GT_BC_Repo
GT Cybersecurity Bootcamp Repository
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Diagram](https://github.com/TAPGAP1/TP_GT_BC_Repo/blob/main/Diagrams/Network_Diagram.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the configuration files may be used to install only certain pieces of it, such as Filebeat.

  - [filebeat-playbook.yml](https://github.com/TAPGAP1/TP_GT_BC_Repo/blob/main/Ansible/filebeat-playbook.yml)
  - [filebeat-config.yml](https://github.com/TAPGAP1/TP_GT_BC_Repo/blob/main/Ansible/filebeat-config.yml)
  
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly functional, in addition to restricting high volumes of traffic to the network.

What aspect of security do load balancers protect? 

 - They help prevent overloading servers by balancing the flow of traffic between them based on a configured algorithm.  If a server is hit by a DDoS attack or becomes unavailable
  the other servers will take over and share the load. 
  
What is the advantage of a jump box?
 - A Jump Box Provisioner is important. The primary purpose of the jump box is to provide you a central management machine for configuration, patching, and maintenance of the machines on your private network. This allows us to monitor and collect logs on a single box. We can also restrict the IP addresses able to communicate with the Jump Box, as we've done here.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.

What does Filebeat watch for?
 - It monitors the log files or locations that you specify and forwards them to Elasticsearch or Logstash for indexing.
  
What does Metricbeat record?
 - It collects metric data from your target servers such as CPU usage or uptime, or memory. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function |               IP Address                  | Operating System |
|----------|----------|-------------------------------------------|------------------|
| Jump Box | Gateway  | 10.0.0.5(private) / 20.106.141.49(public) | Linux            |
| Web-1    | Server   | 10.0.0.6                                  | Linux            |
| Web-2    | Server   | 10.0.0.7                                  | Linux            |
| Web-3    | Server   | 10.0.0.8                                  | Linux            |
| Elk_VM   | Server   | 10.1.0.4(private) / 13.66.207.75(public)  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. 
 Access to this machine is only allowed from the following IP addresses:
 - 66.232.xxx.xxx
 
Machines within the network can only be accessed by the Jump Box Provisioiner.
 
Which machine did you allow to access your ELK VM?
- Jump Box Provisioner
   
What was its IP address?
- 10.0.0.5

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 66.232.xxx.xxx       |
|  Web-1   | No                  | 10.0.0.5             |
|  Web-2   | No                  | 10.0.0.5             |
|  Web-3   | No                  | 10.0.0.5             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

What is the main advantage of automating configuration with Ansible?
 - One advantage of automation is YAML Playbooks. Playbooks allow for a quick setup of the VM without haivng to download and install different services individually. 

The playbook implements the following tasks:
 - Install docker.io 
 - Install pip3 (python3-pip)
 - Increase Virtual Memory
 - Download and launch ELK docker container (sebp/elk:761) w/ published ports 5601, 5044, and 9200
 - Enable docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[docker ps output](https://github.com/TAPGAP1/TP_GT_BC_Repo/blob/main/Linux/ELK_container.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
 - Web-1 (dvwa) 10.0.0.6
 - Web-2 (dvwa) 10.0.0.7
 - Web-3 (dvwa) 10.0.0.8

We have installed the following Beats on these machines:
 - Filebeat
 - Metricbeat

These Beats allow us to collect the following information from each machine:
 - Filebeat is used to collect log files from specific files on remote machines. Examples of Filebeats can be files that are generated by Apache, Microsoft Azure tools, the Nginx web server, and MySQl databases.
 - Metricbeat collects machine metrics. Analysts use these metrics to monitor how healthy a machine is by looking at things like CPU usage or uptime and memory. 

Filebeat

- Copy the filebeat-config.yml file to /etc/ansible .
- Update the filebeat-config.yml file to include the elk private IP on lines 1105 and 1805. 
- Run the playbook, and navigate to http://<elk_public_IP>/app/kibana to check that the installation worked as expected.

Metricbeat

- Copy the metricbeat-config.yml file to /etc/ansible.
- Update the metricbeat-config.yml file to include the ELK private IP in lines 62 and 95.
- Run the playbook, and navigate to http://<elk_public_IP>:5601/app/kibana to check that the installation worked as expected.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

ELK

 - Copy the install-elk.yml file to /etc/ansible
 - Update the Ansible/hosts file to include a "webservers" section and an "elk" section with the private IP of the ELK-VM.
 - Run the playbook, ssh into ELK-VM and run "docker ps" to verify installation worked as expected. *Note* - The status of the ELK container should be "up" on boot. 



Answer the following questions to fill in the blanks:

Which file is the playbook? 

 - install-elk.yml

Where do you copy it?

 - /etc/ansible

Which file do you update to make Ansible run the playbook on a specific machine?

 - Ansible/hosts
 
How do I specify which machine to install the ELK server on versus which to install Filebeat on?

 -  Update the Ansible/hosts file to include a "webservers" section and an "elk" section with the private IP of the ELK-VM.
 
Which URL do you navigate to in order to check that the ELK server is running?

 - http://13.66.207.75:5601
 
