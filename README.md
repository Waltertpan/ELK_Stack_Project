## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
- Diagrams/ELK_Stack_Network_Topology.pdf

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

  - Ansible/install-elk.yml
  - Ansible/filebeat-playbook.yml
  - Ansible/metricbeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

A walkthrough of ELK, Filebeat, and Metricbeat setup can be found in:
-Files/ELK_Filebeat_Metricbeat_Setup_Walkthrough.pdf

Testing and exploring Kibana after setup can be found in:
-Files/Exploring Kibana.pdf

The sample interview question from the project can be found in:
-Files/Interview Questions.pdf

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly fault tolerant, in addition to restricting access to the network.
- Load balancers ensure system availability when a one or more components within the system fail or are overloaded by distributing the load load to redundant components.
- A jump box is a secure admin workstation used as an origination point to connect to other servers in a network for administrative tasks, and used to prevent all the servers in the network from being exposed to the public.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log data and system metrics.
- Filebeat monitors the log files of servers, collects log events, and forwards them to Elasticsearch or Logstash for indexing.
- Metricbeat records metrics and statistics from an operation system and from services running on servers, and forwards them to Elasticsearch or Logstash

The configuration details of each machine may be found below.

| Name       | Function             | Local IP Address | Operating System |
|------------|----------------------|------------------|------------------|
| Jump Box   | Gateway              | 10.0.0.4         | Linux            |
| Web-1      | DVWA Virtual Machine | 10.0.0.5         | Linux            |
| Web-2      | DVWA Virtual Machine | 10.0.0.6         | Linux            |
| Web-3      | DVWA Virtual Machine | 10.0.0.8         | Linux            |
| ELK-SERVER | ELK Stack            | 10.1.0.4         | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 73.151.82.233

Machines within the network can only be accessed by the jump box machine.
- Only the jump box machine can access the ELK-SERVER from 52.250.119.203.

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jump Box   | No                  | 73.151.82.233        |
| Web-1      | No                  | 52.250.119.203       |
| Web-2      | No                  | 52.250.119.203       |
| Web-3      | No                  | 52.250.119.203       |
| ELK-SERVER | No                  | 52.250.119.203       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it improves reliability, consistency, and speed of deployment through the use of infrastructure as code.
- The main advantage of automating configuration with Ansible is the improvement in speed and reduction of human error.

The playbook implements the following tasks:
- Install Docker.io
- Install python3-pip
- Install Docker python module
- Increase available memory by setting vn.max_map_count to 262144
- Download and launch docker elk container
- Enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
- Images/docker_ps_output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6
- 10.0.0.8

We have installed the following Beats on these machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.6
- Web-3 10.0.0.8

These Beats allow us to collect the following information from each machine:
- Filebeat collects log events, which we can provide information about network traffic, usage and other conditions in systems.
- Metricbeat collects metrics on systems and services, which can be used to monitor CPU and memory usage, network traffic, and other metrics in the systems and services.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ELK configuration file to the file directory.
- Update the host file to include the IP address of ELK server and python 3.
- Run the playbook, and navigate to http://ELK-SERVER_public_IP]:5601/app/kibana to check that the installation worked as expected.

Installing ELK from Ansible
- Modify the host file from /etc/hosts to include : [elk]
- Modify the host file from /etc/hosts to include: [ELK-SERVER_local_IP] ansible_python_interpreter=/usr/bin/python3 below [elk]
- Copy the install-elk.yml file to /etc/ansible
- Copy the file ansible.cfg to /etc/ansible/files
- Run the install-elk.yml playbook
- Check that the installation worked by navigating to http://ELK-SERVER_public_IP]:5601/app/kibana
- The following screenshot will display if Kibana successfully launches, Images/Kibana_Webpage.png.
- If there are issues accessing the kibana page above, check Network Security Group Inbound rules on Azure.

Installing Filebeat on the DVWA Container with Ansible
- Make sure the kibana page above is accessible
- Copy the filebeat-playbook.yml file to /etc/ansible
- Copy the file filebeat-config.yml to /etc/ansible/files
- Run the filebeat-playbook.yml playbook
- Check on Kibana that logs are being received

Installing Metricbeat on the DVWA Container with Ansible
- Make sure the kibana page above is accessible
- Copy the metricbeat-playbook.yml file to /etc/ansible
- Copy the file metricbeat-config.yml to /etc/ansible/files
- Run the metricbeat-playbook.yml playbook
- Check on Kibana that logs are being received

ELK, Filebeat, and Metricbeat configuration files location
- Ansible/ansible.cfg
- Ansible/filebeat-config.yml
- Ansible/metricbeat-config.yml

ELK, filebeat, Metricbeat setup walkthrough
- Ansible/ELK_Filebeat_Metricbeat_Setup_Walkthrough.pdf