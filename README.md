## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](CSBootCamp_AzureProject/Images/Project1Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the install-elk.yml file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting unauthorized access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log data and system metrics.

The configuration details of each machine may be found below.

| Name        | Function   | IP Address | Operating System |
|-------------|------------|------------|------------------|
| Jumpbox     | Gateway    | 10.0.0.4   | Linux            |
| Web-1       | Web Server | 10.0.0.5   | Linux            |
| Web-2       | Web Server | 10.0.0.6   | Linux            |
| ELK-StackVM | ELK Server | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My local machine IP

Machines within the network can only be accessed by the Jumpbox.

A summary of the access policies in place can be found in the table below.

| Name        | Publicly Accessible | Allowed IP Addresses       |
|-------------|---------------------|----------------------------|
| Jumpbox     | Yes                 | 10.0.0.5 10.0.0.6 10.1.0.4 |
| Web-1       | No                  | 10.0.0.4            |
| Web-2       | No                  | 10.0.0.4             |
| ELK-StackVM | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it reduces the potential for human error and simplifies the process of configuring multiple machines on a network all at once.

The playbook implements the following tasks:
- install Docker engine, used for running containers
- install pip3, a package used to install Python software
- install the pip package docker.io, a Python client for docker
- downloads the docker container called `sebp/elk:761`

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](CSBootCamp_AzureProject/Images/using_docker_ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1(10.0.0.5)
- Web-2(10.0.0.6)

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors the log files such as a history of web page requests.
- Metricbeat monitors host metrics such as CPU and memory usage of a web server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible/.
- Update the /etc/ansible/hosts file to include a group called '[elk]' and add the private IP of the VM that will host the ELK server.
- Run the playbook, and navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana to check that the installation worked as expected. Use the public IP of your ELK server VM.
