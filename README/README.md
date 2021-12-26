## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/Diagrams/Network_Diagram_ELK.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Cyber Security Project file may be used to install only certain pieces of it, such as Filebeat.

filebeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting access to the network.
- The load balancer is integral to the Availability aspect within the CIA triad. This is because it allows authorized user access to the systems they need. The VMs are accessed through a jump box. It is an important gateway for access as it streamlines the deployment of administration to the VMs in the network as well as restricting access.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat monitors log files and log events then forwards them to be indexed.
- Metricbeat monitors metrics and data from the traffic and VMs then forwards it.

The configuration details of each machine may be found below.

| Name          | Function      | IP Address             | Operating System |
|---------------|---------------|------------------------|------------------|
| Jump Box      | Gateway       | 40.122.113.219         | Linux            |
| Web-1         | Web Server    | 10.0.0.8               | Linux            |
| Web-2         | Web Server    | 10.0.0.9               | Linux            |
| Web-3-ELK     | ELK Server    | 20.121.39.122/10.1.0.4 | Linux            |
| Load Balancer | Load Balancer | 40.122.65.36           | Linux            |
| Home IP       | Remote Access | 67.4.193.29            | MacOS            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address:
- Home IP: 67.4.193.29 through port 5601

Machines within the network can only be accessed by Home IP and the Jump Box Provisioner.
- Jump Box Provisioner can access the ELK server and it's public IP is 40.122.113.219

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses    |
|---------------|---------------------|-------------------------|
| Jump Box      | No                  | 65.4.193.29 SSH port 22 |
| Web-1         | No                  | 10.0.0.7 SSH port 22    |
| Web-2         | No                  | 10.0.0.7 SSH port 22    |
| Web-3-ELK     | No                  | 65.4.193.29 TCP 5601    |
| Load Balancer | No                  | 65.4.193.29 HTTP 80     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows for quick set up of virtual machines and a more flexible network set up.

The playbook implements the following tasks:
- Specify which VMs in a group to configure and gives a remote user access.
- Installs docker with several modules.
- Sets which ports to be available to connect.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/connected_elk.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.8
- Web-2 10.0.0.9

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects logs files and log events. An alert can be set if certain logs have red flags.
- Metricbeat collects system statistics and metrics. An alert can be set if systems are using high volumes of memory.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Ansible installation file to control node.
- Update the config file to include groups with IP addresses of VMs
- Run the playbook, and navigate to Kibana > Add Metric Data > Docker Metrics > Module Status to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it? Install-elk.yml. Copy it to /etc/ansible/
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? Ansible.cfg under [web servers] add the VMs you want to monitor and under [elk] add the VM IP you want to install ELK on. 10.1.0.4 ansible_python_interpreter=/usr/bin/python3
- Navigate to Http://ELK-Server-IP:5601/app/Kibana to check to see if the ELK server is running.
