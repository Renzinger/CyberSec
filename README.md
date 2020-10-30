# CyberSec
A collection of ren works

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!(Images/WK13_Elk_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - install-elk.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.
- The load balancer ensures that work to process incoming traffic will be shared by both vulnerable web servers. Access controls will ensure that only authorized users will be able to connect in the first place.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the VMs on the network, as well as watch system metrics, such as CPU usage; attempted SSH logins; sudo escalation failures; etc.
- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat takes the metrics and stats that it collects and ships them to the output that you specify.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web 1    |Web Server| 10.0.0.9   | Linux            |
| Web 2    |Web Server| 10.0.0.10  | Linux            |
| Web 3    |Web Server| 10.0.0.5   | Linux            |
| ELK-VM   |Monitoring| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 24.20.141.10

Machines within the network can only be accessed by SSH.
- The Jump Box with the ip address of 10.0.0.4 can SSH into the ELK-VM.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | SSH 24.20.141.10     |
| Web 1    | No                  | SSH 10.0.0.4         |
| Web 2    | No                  | SSH 10.0.0.4         |
| Web 3    | No                  | SSH 10.0.0.4         |
| ELK-VM   | Yes                 | SSH 10.0.0.4 24.20.141.10|

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- many of the exact builds can be deployed at once with no errors.

The playbook implements the following tasks:
- Install docker
- Install python-pip
- Install docker module
- Increase virtual memory
- Use more memory
- Download and launch a docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.9 10.0.0.10 10.0.0.5

We have installed the following Beats on these machines:
- filebeat, metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat and Metricbeat include modules that simplify collecting, parsing, and visualizing information from key data sources such as cloud platforms, containers and systems. They will send the gathered information to designated log files.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the yml file to /etc/ansible.
- Update the hosts file to include the ip addresses of the machines being configured by the playbook.
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.


- The playbooks are: install-elk.yml filebeat-playbook.yml
- You can update the hosts file in the ansible directory to specify which machine to run each playbook.
- To access the Kibana page: http://(public ip address of ELK-VM):5601
