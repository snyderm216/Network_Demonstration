# Network_Demonstration
The files in this repository were used to configure the network depicted below.
Network Map.png

These files have been tested and used to generate a live ELK deployment on Azure. 
They can be used in their entirety to recreate the entire deployment pictured above or separated to accomplish subtasks (Such as installing Filebeat).

#TODO Add-in playbook folder


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

