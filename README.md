# Cybersecurity
Information Security repository
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![RedTeam_Network_Diagram](https://github.com/Nbettis1/ELK_Repository/blob/master/Diagrams/RedTeam_Network_Diagram.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Elk installation files may be used to install only certain pieces of it, such as Filebeat.

 [Elk installation files](https://github.com/Nbettis1/ELK_Repository/tree/master/Ansible)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
- Load balancing ensures that the application will be highly reliable, in addition to restricting direct access to the network.
- Load balancers protect the availability of your web servers. 
- The advantage of a jump box is a single vm to access and control all of the necessary network components.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system and system metrics.
Filebeat watches for changes to the file system.
Metricbeat watches for changes to system metrics, like uptime, or data usage.

The configuration details of each machine may be found below.

| Name     | Function   | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.8   | Linux            |
| Web-1    | Web Server | 10.0.0.7   | Linux            |
| Web-2    | Web Server | 10.0.0.6   | Linux            |
| Web-3    | Web Server | 10.0.0.4   | Linux            |
| ELK-1    | ELK Server | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Public IP of network engineer.

Machines within the network can only be accessed by the Jump Box.
- Jump Box 10.0.0.8 

A summary of the access policies in place can be found in the table below.

| Name        | Publicly Accessible | Allowed IP Addresses |
|-------------|---------------------|----------------------|
| Jump Box    | Yes/No              | NE Public IP         |
| Web Servers | No                  | 10.0.0.8             |
| ELK Server  | No                  | 10.0.0.8             |
| Kibana      | Yes                 | NE Public IP         |
| DVWA        | Yes                 | NE Public IP         |

NE Public IP = Network Engineer's Public IP address. Remote access.

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- It is incredibly time effecient.
- Updates only have to be run _once_ via the playbook for every machine updated.

The playbook implements the following tasks:
- Install docker
- Install python3
- Install docker module
- Install Elk data container with specified ports
- Enable Docker Server
- Increase virtual memory in current runtime
- Permanently increase virtual memory on restart

The following screenshot displays the result of running `sudo docker ps` after successfully configuring the ELK instance.

![docker_ps_output](https://github.com/Nbettis1/ELK_Repository/blob/master/Diagrams/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.7 Web-1, 10.0.0.6 Web-2, 10.0.0.4 Web-3

We have installed the following Beats on these machines:
- Metricbeat and Filebeat

These Beats allow us to collect the following information from each machine:
- Metricbeat and Filebeat both contain logs of important data on a linux system. Filebeat collects data related to file configurations on a linux server while Metricbeat collects data about system metrics like uptime, data usage, system usage, etc. 
- If you run a windows server you may run Winlogbeat. Winlogbeat collects Windows logs and would send data related to all windows logs including system logs, security logs, application logs and others. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible.
- Update the hosts file to include the new server IP's and the host name of your choice. (make sure to include 'ansible_python_interpreter=/usr/bin/python3' after the IP)
- Run the playbook, and navigate to the new servers IP via ssh and run docker ps to check that the installation worked as expected.

- install-elk.yml is the elk installatation .yml file. Copy install-elk.yml to the /etc/asnible directory.
- Update the /etc/ansible/hosts/ file with a new hosts name and specific IPs of each vm in the host. Update the .yml file and specify the host to install on. Additionally you can use --limit when running an ansible-playbook to specify a host name if the file does not specify one. You can additionally limit servers within a host this way.
- After installation and allowing Kibana port access to your IP go to http://[your.ELK-VM.External.IP]:5601/app/kibana.
