Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/kpkelsey/Elk_Stack_Project/blob/main/ELK_Stack_Network_Diagram.png?raw=true

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the /etc/ansible/(file_name)-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.
Ansible Playbooks live in the /etc/ansible/ folder.

ansible-playbook.yml
hosts.yml
elk-playbook.yml
filebeat-playbook.yml
metricbeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly efficient, in addition to restricting unwanted access to the network.

What aspect of security do load balancers protect? What is the advantage of a jump box?_ A load balancer protects the availability of the intended webserver to distribute traffic and help protect against DDoS attacks. The advantage of utilizing a jump box is that it provides a secure computer to have everyone connect through.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system and system resources.
What does Filebeat watch for? Filebeat watches the logging of changes to the local system files.
What does Metricbeat record? Metricbeat allows an administrator to track CPU/RAM usage, and network utilization within the log files.

The configuration details of each machine may be found below.
| Name     |  Function   | IP Address   | Operating System |
|----------|------------ |------------- |------------------|
| Jump Box |Gateway      | 10.0.0.1     | Linux            |
| Web-1    |Webserver    | 10.0.0.8     | Linux            |
| Web-2    |Webserver    | 10.0.0.9     | Linux            |
| ELK      |Kibana Host  | 10.1.0.4     | Linux            |
| Load-Bal |Load Balancer|13.66.185.179 | N/A              |

### Access Policies
The machines on the internal network are not exposed to the public Internet. 
Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

Machines within the network can only be accessed by My IPV4.
A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | My IPV4              |
| Web-1    | No                  | 10.0.0.12            |
| Web-2    | No                  | 10.0.0.12            |
| ELK VM   | TCP/Ports 80 & 5601 | 10.0.0.12 My IPV4    |

### Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

What is the main advantage of automating configuration with Ansible?_ The ansible-playbook can be used to re-deploy the same working environment to protect against any emergencies or disasters. It also makes new servers on the network easy to setup. No manual configuration is required.

The playbook implements the following tasks:

ELK can be installed in 5 easy steps:
Download and install Docker
Install python-pip3 and the “pip” docker module
The size of the vm.max_map_count variable to  ‘262144’#sysctl -w vm.max_map_count=262144
Install ELK inside the docker container
Ensure that Docker and ELK start with system boot processes

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/kpkelsey/Elk_Stack_Project/blob/main/docker_ps_output.png.png?raw=true

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

The ELK server has been configured to monitor the following machines:
Web-1 10.0.0.8
Web-2 10.0.0.9

The following Beats have been installed on these machines.
Web-1: Filebeat & Metricbeat
Web-2: Filebeat & Metricbeat

These Beats allow us to collect the following information from each machine:

Filebeat monitors the system for local file system changes. Metricbeat logs CPU/RAM Utilization. The Metricbeat logs can be utilized to ensure the server is never burdened or overworked. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
SSH into the control node and follow the steps below:

Edit the /etc/ansible/ansible.cfg file, line rmote_user=USERNAME to reflect the remote account being used to execute playbooks.
Update the /etc/ansible/hosts.yml file and add the group or groups the packages need to be installed on. In this instance, two new groups were added, {webservers} and {elk} and the corresponding IP addresses.
Run the playbook, and navigate to the remote hosts to verify that the installation worked as expected.
The playbooks are located in /etc/ansible, and it is recommended to copy them to a local machine.
To verify your instance of ELK is functioning properly, go to http://[ELK-PUBLIC-IP]:5601/app/kibana and replace [ELK-PUBLIC-IP] with the IP address of the ELK VM.

