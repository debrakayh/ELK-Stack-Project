## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![diagram](images\RedTeam-Network.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yaml file may be used to install only certain pieces of it, such as Filebeat.

  [](scripts\elk-playbook.yml)
  [](scripts\filebeat-playbook.yml)
  [](scripts\filebeat-config.yml)
  [](scripts\metricbeat-playbook.yml)
  [](scripts\metricbeat-config.yml)
  
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly 

        available, 
in addition to restricting 

        the public traffic
to the network.

What aspect of security do load balancers protect? 
 
 -      Defends an organization against distributed denial-of-service (DDoS) attacks.
 -      Creates access controls that gives correct permissions to users.
 
 
What is the advantage of a jump box?_ 
 
-       Updates only need to be put on that single system and be deployed to the VMs it connects to.
-       Makes troubleshooting easier.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the 

        files 
and 
        
        system metrics.
What does Filebeat watch for?

        files and data
What does Metricbeat record?

        system metrics

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1, 13.90.19.78   | Linux            |
| Web-1    |    VM    | 10.0.0.5   | Linux            |
| Web-2    |    VM    | 10.0.0.6   | Linux            |
| ELK      |    ELK   | 10.1.0.5, 104.42.252.128   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Gateway machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

        Local Host (my public IP); 
        Web-1 10.0.0.5; 
        Web-2 10.0.0.6

Machines within the network can only be accessed by the load balancer.
Which machine did you allow to access your ELK VM?
 
        Jumpbox 
What was its IP address?

        13.90.19.78

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses  |
|----------|---------------------|---------------------- |
| JumpBox  |  Yes                |My public IP           |
| ELK      |  Yes                |10.1.0.5/My public IP  |
| Web-1    |  No                 |10.0.0.0/16-10.1.0.0/16|
| Web-2    |  No                 |10.0.0.0/16-10.1.0.0/16|
### Elk Configuration


Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

        It avoids human error
        enables automation for more efficient changes
        Saves coding time
        

What is the main advantage of automating configuration with Ansible? 

        you only have to do it once
        avoids errors

The playbook implements the following tasks:
In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
 
        install docker.io
        install pip3
        increase memory
        download and launch container
        restart docker on reboot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![screenpring](images\docker-ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
List the IP addresses of the machines you are monitoring_

        Web-1 10.0.0.5  
        Web-2 10.0.0.6
We have installed the following Beats on these machines:

Specify which Beats you successfully installed_
 
        filebeats and metricbeats

These Beats allow us to collect the following information from each machine:
In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

        - Filebeats collects data about open files how often they've been accessed and by whom.
        - Metricbeats collects data about the VM metrics and performance... memory usage, CPU usage

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the 

        - config file 
  to 

        /etc/ansible/file.

- Update the 
 
        - config 
  file to include 

        the ELK server's private IP address 10.1.0.5
- Run the playbook, and navigate to 
        
        Kibana 
  to check that the installation worked as expected.

Answer the following questions to fill in the blanks:_
- _Which file is the playbook? 

        ELK-playbook.yml 
Where do you copy it? 

        /etc/ansible
Which file do you update to make Ansible run the playbook on a specific machine? 

        /etc/ansible/hosts
       
  How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ 

        by typing in the IP address of the server you want to install on
Which URL do you navigate to in order to check that the ELK server is running? 

        http://104.42.252.128:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._ 

        cd /etc/ansible/ 
        nano playbook.yml 
        ansible-playbook playbook.yml
        http://104.42.252.128:5601
