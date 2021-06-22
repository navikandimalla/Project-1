# Readme 

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Name of file: Project 1 - Network Diagram.png



These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly avaiable, in addition to restricting in-bound access to the network.
Load Balancing ensures availability to the web-servers which is the availability aspect of security.They also protect from DDoS attacks by shifting attack traffic.

The main advantage of using a JumpBox is having single starting point for administrative tasks. Also this can set up the JumpBox as a Secure Admin Workstation (SAW). As In order to conduct administrative tasks administrators are required to access the JumpBox before accessing the other servers.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system traffic and system metrics.

	Filebeat watches for log files/locations and collect log events. " Filebeat uses a backpressure-sensitive protocol when sending data to Logstash or Elasticsearch to account for higher volumes of data. If Logstash is busy crunching data, it lets Filebeat know to slow down its read. Once the congestion is resolved, Filebeat will build back up to its original pace and keep on shippin'"(Filebeat: Lightweight Log Analysis & Elasticsearch)(" https://www.elastic.co/beats/filebeat")
	Metricbeat records metrics and statistical data from the operating system and from services running on the server. "Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash" (Metricbeat: Lightweight Shipper for Metrics) ("https://www.elastic.co/guide/en/beats/metricbeat/current/metricbeat-overview.html")
	


The configuration details of each machine may be found below.

| Name       		| Function              | IP Address     | Operating System |
|-----------------------|-----------------------|----------------|------------------|
| Jump-Box-Provisioner 	| GATEWAY               | 138.91.157.14  | LINUX            |
| WEB-1      		| WEBSERVER             | 10.2.0.5       | LINUX            |
| WEB-2      		| WEBSERVER             | 10.2.0.6       | LINUX            |
| ELK-SERVER 		| MONITORING/ELK Server | 10.1.0.4       | LINUX            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

	* Personal IP Address/ Local Host IP Address
	  My Local IP (142.118.187.**** )

Machines within the network can only be accessed by SSH.

	* The ELK-Server is only accessible by SSH from the JumpBox and via web access from Personal IP Address

Machines within the network can only be accessed by the Jumpbox-Provsional.The IP address is 10.1.0.4


A summary of the access policies in place can be found in the table below.


| NAME       | PUBLICLY ACCESSIBLE  | ALLOWED IP ADDRESS                                            |
|------------|----------------------|---------------------------------------------------------------|
| JUMP BOX   | YES(from Local Host) | My Local IP (142.118.187.*****)    					                  |
| WEB-1      | NO                   | 10.1.0.4                                                      |
| WEB-2      | NO                   | 10.1.0.4                                                      |
| ELK-SERVER | NO                   | 10.1.0.4                                                      |




### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

It is simple, powerful and Agentless  ( https://www.ansible.com/overview/it-automation )

Following are the main advantages of the automating configurations with Ansible:

Simple to Learn : The foremost mention among advantages of Ansible refers to its simplicity.It is easy to learn, and so, users could learn to use Ansible quickly along with better productivity. Ansible receives the support of comprehensive and easily interpretable documentation.

Easily Understandable Programming Language : One of the prominent advantages of Ansible also refers to the language in which it is written. It is in human-readable language and serves as the basis for Ansible. 

No Dependency on Agents : The next important addition among the benefits of Ansible refers to its agentless nature. Ansible manages all the master-agent communications through Standard SSH or Paramiko module. 

Playbooks are written in YAML : The use of Playbooks in Ansible is also another reason for the major advantages of Ansible. Playbooks are Ansible configuration files, and the language for writing them is YAML.

Ansible Galaxy: Another notable entry in the Ansible best practices refers to the Ansible Galaxy. Ansible Galaxy is a portal that acts as the central repository for locating, reusing, and sharing Ansible-related content. The best advantage of Ansible Galaxy is in the example of downloading reusable Roles for installing application or server configuration. The downloads are ideal for use in a particular user’s playbooks and can contribute substantially to an increase in deployment speed.
 
(" https://www.whizlabs.com/blog/ansible-advantages-and-disadvantages/ ")


The playbook implements the following tasks:

- Install-elk.yml: This playbook is used to configure the ELK server. It installs the downloads and installs docker, and the pulls correct container into ELK VM. It configures the machine to use more memory. And has a 
restart policy in place start elk container every time the machine boots. It configures that ports 5601 to be used to host the Kibana GUI.

- filebeat-playbook.yml: The playbook configures filebeat for the kibana GUI. This playbook downloads, installs and configures filebeat correctly. It starts the filebeat service, and has a restart policy in place for it to run
on systemboot

- metricbeat-playbook.yml: The playbook configures metricbeat for the kibana GUI. This playbook downloads, installs and configures metricbeat correctly. It starts the metricbeat service, and has a restart policy in place for it to run
on systemboot


Install docker.io
Install pip3
Install Docker python module
Increase virtual memory
Download and launch/configure a docker container


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.




### Target Machines & Beats


This ELK server is configured to monitor the following machines:

+------+------------+
| Name | IP Address |
+------+------------+
| WEB1 | 10.2.0.5   |
+------+------------+
| WEB2 | 10.2.0.6   |
+------+------------+

We have installed the following Beats on these machines:

Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:

Filebeat - collects data about the file system; collects log events specified by log files and location.

Metricbeat - collects machine metrics, such as uptime.and statistics from servers. 
The metrics could vary from system resources to metrics of services being run on the given system.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 


SSH into the control node and follow the steps below:
	Copy the filebeat-config.yml and metricbeat-config.yml file to /etc/ansible/files.
	Update the configuration file to include webserver and elk
	Run the playbook, and navigate to ELK-Serverto check that the installation worked as expected.


- _Which file is the playbook? Where do you copy it?
	elk-playbook.yml, filebeat-playbook.yml, metricbeat-playbook.yml. It is copied into /etc/ansible/roles

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- The host file is updated to make Ansible run the playbook on a specific machine. We specify the [elk] header followed by the IP of machine ensure ELK-stack is installed in the correct machine. We declaree the private IPs 
of Web-1 and Web-2 under [webservers] to ensure filebeat is installed on the correct machine. 

-_Which URL do you navigate to in order to check that the ELK server is running?
- We navigate following to access the kibana-GUI
http://20.151.117.30/:5601/app/kibana#/ ( Unique to me )


_Few Commands the user will need to run to download the playbook, update the files, etc._

-ssh azadmin@JumpBox(PrivateIP)
-sudo docker container list -a - to Locate the ansible container
-sudo docker start Container ID/Conatiner name
-sudo docker attach Container ID/Conatiner name
-cd /etc/ansible
-ansible-playbook elk-playbook.yml (Installs and Configures ELK-Server)
-ansible-playbook filebeat-playbook.yml (Installs and Configures Beats)
