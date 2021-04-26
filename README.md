This list of files has been tested and executed in order to estagblish live ELK deployments on Azure. Files may be used to recreate the entirety of the deployment shown in the Network Diagram file.

This document contains the following details:

-Description of the Topology

-Access Policies

-ELK Configuration

-Target Machines and Beats

-Using the Playbooks


DESCRIPTION OF THE TOPOLOGY


The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web App.

Load balancers enable the application to be readily available, while also restricting inbound access to the network.

A load balancer effectively distributes traffic from clients across multiple servers without the need for the client to understand how many servers are in use or how they are configured. Load balancers provide additional security, resilience and simplify website scaling.

What is the advantage of a jump box?

A jump box is a secure computer that is the basis for launching any administrative task or the original point to connect to other servers or suspicious files.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the jumpbox and system network. Filebeat watches for file changes on the machine. Metricbeat collects metrics from both the operating system and from services running on the server.

Configuration details of each Virtual Machine. (Name, Function, IP Address, Operating System)

Jump Box is a gateway. IP=10.0.0.5	Operating System=Linux

Web-1	is a webserver.  IP=10.0.0.6	Operating System=Linux

Web-2	is a webserver	 IP=10.0.0.7	Operating System=Linux

Elk-Server is for monitoring.  IP=10.1.0.6	Operating System=Linux


ACCESS POLICIES

The machines on the internal network are not exposed to the public Internet.

Only the jump box provisioner machine may accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

5061 Kibana Port
Machines within the network can only be accessed by jump box provisioner.

Which machine did you allow to access your ELK VM?

My IP Address: 104.172.224.176

A summary of the access policies in place can be found in the list below.

NAME=Jump Box	PUBLICLY ACCESSIBLE=Yes	IP=72.179.7.89

NAME=Web-1	PUBLICLY ACCESSIBLE=No	IP=10.1.0.6

NAME=Web-2	PUBLICLY ACCESSIBLE=No	IP=10.1.0.6

NAME=ELK-Server	 PUBLICLY ACCESSIBLE=No	IP=10.1.0.6


ELK CONFIGURATION

Ansible is an open-source tool which means anybody can use it for free. It is a great tool because it is powerful enough to run complicated modelings and you have the ability to edit the whole app environment as you wish no matter where it is deployed. In addition, it requires no other software assistance which saves both time and local computer memory.

The playbook implements the following tasks: 

-Install docker.io

-Install pip3

-Install Docker python module

-Increase virtual memory

-Download and launch a docker


TARGET MACHINES & BEATS

This ELK server is configured to monitor the following machines: 

Web-1	IP=10.0.0.6

Web-2	IP=10.0.0.7

The following beats are installed:

Filebeat - collects data about the file system.

Metricbeat - collects machine metrics.


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
