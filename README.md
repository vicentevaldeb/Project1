ELK STACK PROJECT

TASK: Build a log management platform using the open-source Elasticsearch, LogStash, and Kibana (“ELK”) Stack Tools. 

Contents: 
Introduction and Overview
Topology
Description of Topology
Access Policies
ELK Configuration
Target Machines and Beats
Using the Playbook



INTRODUCTION AND OVERVIEW 

This list of files has been tested and executed in order to establish live ELK deployments on Azure. Files may be used to recreate the entirety of the deployment shown in the Network Diagram file.

Steps to follow: 
Set up a virtual network with appropriate firewall protections. 
Protect the cloud network  with a firewall. 
Deploy virtual computers to the cloud network (Jumpbox and Prov).
Access VNet from Jumpbox.
Install and run containers using Docker.
Set up Ansible connections to VMs inside the VNet.
Write Ansible playbooks to configure VMs. 
Create load balancers on Azure platform.
Create a firewall and load balancer rules to forward traffic to the correct virtual machines.
Deploy containers using Ansible and Docker.
Deploy Filebeat using Ansible.
Deploy ELK Stack on a server.
Diagram network and create a README file. 



TOPOLOGY

https://github.com/vicentevaldeb/Project1/blob/main/NET%20DIAGRAM.png



DESCRIPTION OF THE TOPOLOGY

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web App.

Load balancers enable the application to be readily available, while also restricting inbound access to the network.

A load balancer effectively distributes traffic from clients across multiple servers without the need for the client to understand how many servers are in use or how they are configured. Load balancers provide additional security, resilience and simplify website scaling.

What is the advantage of a jump box?

A jump box is a secure computer that is the basis for launching any administrative task or the original point to connect to other servers or suspicious files.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the jumpbox and system network. Filebeat watches for file changes on the machine. Metricbeat collects metrics from both the operating system and from services running on the server.

Configuration details of each Virtual Machine are found on the following link. (Name, Function, IP Address, Operating System)

https://github.com/vicentevaldeb/Project1/blob/main/Config%20details.png



ACCESS POLICIES

The machines on the internal network are not exposed to the public Internet.

Only the jump box provisioner machine may accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

The ELK VM is only accessible through SSH and port 22 through the Jumpbox VM and through the 5061 Kibana Port from the Host Machine.

Machines within the network can only be accessed by jump box provisioner.

A summary of the access policies in place can be found in the link below.

https://github.com/vicentevaldeb/Project1/blob/main/Access%20policies.png



ELK CONFIGURATION

Ansible is an open-source tool which means anybody can use it for free. It is a great tool because it is powerful enough to run complicated modelings and you have the ability to edit the whole app environment as you wish no matter where it is deployed. In addition, it requires no other software assistance which saves both time and local computer memory.

The playbook implements the following tasks: 

-Install docker.io

-Install pip3

-Install Docker python module

-Increase virtual memory

-Download and launch a docker

https://github.com/vicentevaldeb/Project1/blob/main/docker%20command%20line.png



TARGET MACHINES & BEATS

This ELK server is configured to monitor the following machines: 

Web-1	IP=10.0.0.6

Web-2	IP=10.0.0.7

Web-3 IP=10.0.0.8

The following beats are installed:

Filebeat - collects data about the file system.

Metricbeat - collects machine metrics.


FILEBEAT monitors log files and locations that are specified, collecting the log events and forwarding them to Elasticsearch or Logstash. 

https://github.com/vicentevaldeb/Project1/blob/main/filebeat%201.png

https://github.com/vicentevaldeb/Project1/blob/main/filebeat%202.png



METRICBEAT periodically collects metrics from the operating system and services running on the server. Metrics and stats are sent to the specified output (Elasticsearch or Logstash). 

https://github.com/vicentevaldeb/Project1/blob/main/metricbeat%201.png

https://github.com/vicentevaldeb/Project1/blob/main/metricbeat%202.png



USING THE PLAYBOOK

NOTE: First set up a Azure portal through Azure Services.

-SSH into the control node (ssh -i [publickey] [azureusername@JumpboxPublIP])

-Copy the playbook files to the Ansible Control Node.

-Change directories to /etc/ansible ($ cd /etc/ansible)

-Make a file directory ($ mkdir files)

-Clone files onto /etc/ansible ($ git clone https://github.com/vicentevaldeb/Project1.git)

-Copy playbooks ($ cp /Project-1/ReadMe/Playbooks/*)

-Update the hosts file to include webserver and elk.

-Edit the hosts file to update and to make Ansible run the playbook on a specific machine, specifying which machine to install the ELK server on and which to install Filebeat onto.

-Run the playbook, and navigate to Kibana (http://[Host IP]/app/kibana#/home) to check that the installation worked as expected.

-Change directories to /etc/ansible ($ cd /etc/ansible)

$ ansible-playbook install_elk.yml elk

$ ansible-playbook install_filebeat.yml webservers

$ ansible-playbook install_metricbeat.yml webservers

Check that the ELK server is running: http://[Host IP]/app/kibana#/home
