# Network_Demonstration
The files in this repository were used to configure the network depicted below.
Network Map.png

These files have been tested and used to generate a live ELK deployment on Azure. 
They can be used in their entirety to recreate the entire deployment pictured above or separated to accomplish subtasks (Such as installing Filebeat).

#https://github.com/snyderm216/Network_Demonstration/tree/main/YAML_Playbooks


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

This setup includes multiple web servers accessed through a load balancer for normal web traffic. 
The administrative side is accessed through a jumpbox.

This configuration ensures that the application will have better availability under load and still restricts unauthorized access to the internal network.
Load balancers are an integral step in ensuring that the setup is more robustly able to withstand high volumes of web traffic including malicious traffic (e.g. Denial Of Service style attacks).
Having a jumpbox ensures that all administrative traffic comes through a very specific, secure, point of entry. This reduces the surface area available for attacks.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the server activity and system logs.
Filebeat centralizes log files for easy collation. 
Metricbeat "collects metrics from systems and services". This allows for monitoring the activity of the webservers themselves.
The combination of these tools deployed on the ELK server provides data in a readily available format

The configuration details of each machine may be found below.
| Name                 | Function    | IP Address | Operating System |
|----------------------|-------------|------------|------------------|
| Jump-Box-Provisioner | Gateway     | 10.0.0.1   | Linux            |
| Web1                 | Webserver   | 10.0.0.5   | Linux            |
| Web2                 | Webserver   | 10.0.0.6   | Linux            |
| ELK-Server           | ELK Server  | 10.1.0.4   | Linux            |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK-Server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My personal IP

Machines within the network can only be accessed by SSH from the Charming Varahamihira container situated on the Jump-Box VM.

A summary of the access policies in place can be found in the table below.

| Name        | Publicly Accessible | Allowed IP Addresses |
|-------------|---------------------|----------------------|
| Jump Box    | Yes                 | Personal IP          |
|  Web1       | No                  | Any                  |
|  Web2       | No                  | Any                  |
| Elk-Server  | Yes                 | Personal IP          |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because future deployments will be far faster and will start from a consistent base.

The playbook implements the following tasks:
- Installing and configuring the docker module with an image for the DVWA
- Installing the ELK stack to monitor the activity on these virtual machines
- Installing Filebeat and Metricbeat to pass logs and data to the ELK stack

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-10.0.0.5 (Web1)
-10.0.0.6 (Web2)

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat will allow the user to view log activity from the observed machines and will send these to Logstash.
- Metricbeat makes sustem metrics such as RAM usage visible

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the YAML file to the target VM.
- Update the YAML file to include the IP addresses of the machines that will need updating
- Run the playbook, and navigate to the target VMs to check that the installation worked as expected.

The Ansible Playbook file is the YAML file that will need to be copied to /etc/ansible in the host/controlling machine, in this setup, the Jump-Box container.
To target a machine to run an Ansible playbook, the easiest method is to update the host config file located in /etc/ansible/hosts and create a new host group that contains the IP address of the targeted machines inside of a group. Then, using the appropriate group in the YAML file header.

THe ELK-Server had not been setup with a static IP in this deployment, but it is importqnt to note that in order to access it port 5601 needs to be specified as the connecting port (e.g. x.x.x.x:5601)

