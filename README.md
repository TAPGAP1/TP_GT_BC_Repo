# TP_GT_BC_Repo
GT Cybersecurity Bootcamp Repository
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

#/c/Users/1troy/TP_GT_BC_Repo/Diagrams

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the configuration files may be used to install only certain pieces of it, such as Filebeat.

  - filebeat-playbook.yml
  - filebeat-config.yml
  
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
  -They help prevent overloading servers by balancing the flow of traffic between them.  If a server is hit by a DDoS attack or becomes unavailable
  the other servers will take over and share the load. 
What is the advantage of a jump box?
  -A Jump Box Provisioner is important. It prevents webserver VMs from being exposed by a public IP Address. This allows us to monitor and collect logs on a single box. We can also restrict the IP addresses able to communicate with the Jump Box, as we've done here.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
What does Filebeat watch for?
  -Filebeat collects data about the file system. 
 What does Metricbeat record?
  -Metricbeat collects machine metrics such as uptime or cpu usage. 

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
-66.232.xxx.xxx
Machines within the network can only be accessed by the Jump Box Provisioiner.
Which machine did you allow to access your ELK VM?
  -Jump Box Provisioner
What was its IP address?
  -10.0.0.5

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
  -One advantage of automation would be YAML Playbooks. It allows for setup in minutes using OpenSSH without having to go to each webserver individually. 

The playbook implements the following tasks:
-Install docker.io 
-Install pip3 (python3-pip)
-Increase Virtual Memory
-Download and launch ELK docker container (sebp/elk:761) w/ published ports 5601, 5044, and 9200
-Enable docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
