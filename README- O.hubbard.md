## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(https://github.com/olivianm1/Project-1-Cloud/blob/master/Diagrams/Network%20Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ELK file may be used to install only certain pieces of it, such as Filebeat.

  - __elk.playbook.yml__

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly __available and responsive__, in addition to restricting load __access__ to the network.
- __The aspect of security that load balancers protect is availability. The advantage of a jumpbox is that is acts like a gateway inbetween the internet and the VMs. This allows for easier focus on interactions between the internet and the jumpbox so monitioring and securing is streamlined.__

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system logs.
- __What does Filebeat watch for? Filebeat watches for data affiliated with the file system by collecting logs for files.__
- __What does Metricbeat record? Metricbeat records metrics that mesure the health of a system reagrding various things such as usage time and load usage.__

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    |Web Server| 10.0.0.5   | Linux            |
| Web-2    |Web Server| 10.0.0.6   | Linux            |
| ELK      | Logging  | 10.1.0.5   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox virtual machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- __104.214.55.129__

Machines within the network can only be accessed by Jump Box ansible containers.
- __The machine that I allowed access to my ELK VM is the Jump Box ansible container; IP 10.0.0.4.__

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses               |
|----------|---------------------|------------------------------------|
| Jump Box | Yes                 | 13.65.168.36,73.166.131.51         |
|Web-1	   | No                  | 10.0.0.4                           |
|Web-2     | No                  | 10.0.0.4                           |
|ELK       | No			             | 13.65.168.36, 73.166.131.51        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because... 
- __The main adavantage of automating configuration with anisble is that user error is diminshed.__

The playbook implements the following tasks:
- __Install docker, python3-pip, and docker module.__
- __Increase virtual memory of the docker module.__
- __Lists the ports the ELK runs on.__ 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(https://github.com/olivianm1/Project-1-Cloud/blob/master/ansible/docker%20ps%20screenshot.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- __Web-1: 10.0.0.5, Web-2: 10.0.0.6__

We have installed the following Beats on these machines:
- __I successfully installed filebeat and metricbeat.__

These Beats allow us to collect the following information from each machine:
__Filebeat was installed and logs information about file systems. For example you can see when and what files have been changed.__
__Metricbeat was installed and measure CPU usuage. For example you can the amount of inbound traffice in quanitative values.__

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- __Copy the configuration file to the /etc/ansible folder.__
- __Update the configuration file to include VMs IP.__
- __Run the playbook, and navigate to kibana to check that the installation worked as expected.__

_TODO: Answer the following questions to fill in the blanks:
- _Which file is the playbook? Where do you copy it?_ __The yaml file is the playbook and you copy it to the /etc/ folder.__
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ __The ansible configuration file is used to update. Specify hosts in order to specify which machine to install the ELK server on versus which to install Filebeat.__
- _Which URL do you navigate to in order to check that the ELK server is running? __The url used to navigate in order to check that the ELK server is running is (Elk IP addess):5601/app/kibana.__

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
- __ssh azureuser@JumpBoxPublicIP__
 - __ssh-keygen__
 - __curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > filebeat-configuration.yml__
 - __curl https://gist.githubusercontent.com/slape/58541585cc1886d2e26cd8be557ce04c/raw/0ce2c7e744c54513616966affb5e9d96f5e12f73/metricbeat > metricbeat-config.yml__
 - __sudo su__
 - __Docker start confident_mclean__
 - __Docker attach confident_mclean__
 - __nano filebeat-configuration.yml__
 - __nano metricbeat-config.yml__
 - __nano elk.playbook.yml__
 - __nano filebeat.playbook.yml__
 - __nano metricbeat.yml__
 - __ansible-playbook elk.playbook.yml__
 - __ansible-playbook filebeat.playbook.yml__
 - __ansible-playbook metricbeat.yml__
