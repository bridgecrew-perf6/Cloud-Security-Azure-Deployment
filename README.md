# Cloud-Security-Azure-Deployment
This is a basic cloud deployment showcasing security topologies use of jump-Box provisioner &amp; ELK server.
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
Diagrams/Cloud_Azure_Deployment_v2.pdf

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above.
The files need to be organized as shown below on the ansible directory in order to work as required to recreate the enviroment.

![ansible_file_hierarchy](https://user-images.githubusercontent.com/70111682/169720577-576e71e0-7ee2-4565-b96e-8c4b48200f74.png)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available (redudancy scheme), in addition to restricting traffic to the network:

- Load Balancers play an important role on securing cloud computing, given the off-load function that defends organization against distributed attacks (DDoS)
- At the L4 load balancer directs traffic based on data from network inbounds and transport layer protocols such as IP and TCP in addition to this at the L7 adds content switching to load balancing which allows routing decisions based on attributes like HTTP header and HTML form data.

The advantage of a jump box relays on the fact that is used as a system tool that prevents direct connection from the public network to the security zone in addition to this on the management side a jump box becomes a tool that could streamline management updates to the security zone trough the use of ansible and docker containers that keep the security zone up to date at minimum effort with scalability proportions.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the work-load and system logs.
- Filebeat is a lightweight tool that forwards and centralize log data. Installed as a component on targets, Filebeat monitors the log files or locations specify on the config files and then collects log events, and forwards them to Elasticsearch for visulaization.

- Metricbeat takes the metrics and statistics that are collected and ships them to the output that is specified on the config files, such as Elasticsearch can provide updated data visualization. Metricbeat helps monitor the VMs on the secure zone by collecting metrics from the system and services running on the machines such as DVWA.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name                 | Function           | IP address     | Operating System     | Size                                 |
|----------------------|--------------------|----------------|----------------------|--------------------------------------|
| jump-Box-Provisioner | Gateway server     | local:10.0.0.4 | Linux (ubuntu 20.04) | Standard B1s (1 vcpu, 1 GiB memory)  |
| ELK Server           | ELK Monitor        | local:10.1.0.4 | Linux (ubuntu 20.04) | Standard B2s (2 vcpus, 4 GiB memory) |
| VM                   | Secure Zone member | local:10.0.0.X | Linux (ubuntu 20.04) | Standard B1ms (1 vcpu, 2 GiB memory) |


### Access Policies
The machines on the internal network are not exposed to the public Internet. 

Only the jump-Box-Provisioner machine can accept connections from the Internet. Management-Access to this machine is only allowed from the <local-management>IP address.

Machines within the network can only be accessed by SSH p22 connections from Jump-Box-Provisioner.
  
- ELK server can be acceessed via SSHp22 from Jump-Box-Provisioner and also ELK can be accessed from <local-management> IP address trough p5601. 

A summary of the access policies in place can be found in the table below.

| Server_name     | Access_Type | Priority | Source            | Destination     |
|-----------------|-------------|----------|-------------------|-----------------|
| ELK Server      | port 5601   | 1100     | <local_ipaddress> | Virtual Network |
| ELK Server      | port 22     | 1000     | Any               | Virtual Network |
| Jump-Box Server | port 22     | 400      | <local_ipaddress> | Virtual Network |
| Jump-Box        | port 80     | 500      | <local_ipaddress> | Virtual Network |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- There are several advantages of performing configuration using ansible such as:
  
  1. Repeatbility and Reproducibility of the set up, using a script is less prone to errors and in case of errors is easy to find since is a single source.
  2. Scalability, in both size and feature set can easely scale from a few to thousands machines in case the deployment grows exponentially and future evolution.
  3. Documentation, is a form of documentation as sourcesafe.

The playbook implements the following tasks:
- Install the following resources in order to perform ELK stack installation: docker.io, python3, docker python Module.
- Adjust memory setting given ELK is system memory demanding.
- download and launch docker elk container and publish access in the following ports:
  
  -  5601:5601
  -  9200:9200
  -  5044:5044
  
 - Enable docker service after reboot, (very important).

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK_docker_ps_v1](https://user-images.githubusercontent.com/70111682/169726676-f646364a-1119-4381-84e7-d603590d30d5.png)

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
