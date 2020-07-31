# week13
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Virtual Machine Diagram](https://github.com/katgoods/week13/blob/master/Diagrams/VM_wELK.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Anisble folder may be used to install only certain pieces of it, such as Filebeat.

  - [Ansible-Playbook files](https://github.com/katgoods/week13/tree/master/Ansible)

This folder contains the following details:

- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting access to the network.

- Load balancers can help prevent a Denial of Service attack by managing traffic to servers. If one server is down, it can divert traffic to another server. A benefit for a jump box is that they provide a single point for connecting to (and managing) multiple machines. If only the jump box is allowed to connect to machines behind a netwrok security group, that is only one point to protect rather than exposing multiple points to attackers.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the server and system files.

- Filebeat ships log files from specified locations and forwards them to the ELK stack. 
- Metricbeat monitors traffic on your servers (CPU, Memory Usage, Disk Space used) by container.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | VM       | 10.0.0.5   | Linux            |
| Web-2    | VM       | 10.0.0.6   | Linux            |
| Web-3    | VM       | 10.0.0.7   | Linux            |
| ELK-VM   | VM       | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 67.189.23.45

Machines within the network can only be accessed by the Jump Box.

- Which machine did you allow to access your ELK VM? JumpBoxProvisioner
- What was its IP address? 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 67.189.23.45         |
| ELK-VM   | No                  | 10.0.0.4             |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |
| Web-3    | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?
  Ansible allows you to easily scale your containers and manage them (instead of managing one at a time).


The playbook implements the following tasks:
- TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install Docker
- Install Pip3
- Checks on memory space
- Downloads and launces the Elk Docker Container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker ps Image](https://github.com/katgoods/week13/blob/master/Images/ELK-dockerps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6
- 10.0.0.7

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:
- Filebeats collect log data and changes made for the VMs. Filebeats can show IPs from inbound traffic, Geolocation, Requests being made, etc.
- Metricbeats collects activity and status of the connected VMs. Here you can see CPU, memory usage, number of containers, etc.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Ansible file to etc/ansible once logged into Jumpbox>AnsibleVM.
- Update the hosts file to include the webserver IP addresses and the webservers group
- Run the playbook, and navigate to the Virtual Machine to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? [Ansible Playbook](https://github.com/katgoods/week13/blob/master/Linux/ansible.cfg) Where do you copy it? /etc/ansible
- Which file do you update to make Ansible run the playbook on a specific machine? Hosts file.
- How do I specify which machine to install the ELK server on versus which to install Filebeat on? Add a group in the hosts file for the ELK machine(s) and include the IP address(es).
- Which URL do you navigate to in order to check that the ELK server is running? <http://40.112.69.201:5601/app/kibana#/home>

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
For Filebeat playbook:
- the command to download the .deb file: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat
- Install the .deb file: dpkg -i filebeat-7.6.1-amd64.deb
- In the command line to run the filebeat playbook, type: ansible-playbook filebeat.yml
