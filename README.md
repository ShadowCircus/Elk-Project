## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Click here for a diagram of the network](https://drive.google.com/file/d/14akl_F5LcczJaZdBSShIs3rVBIMBGoVG/view?usp=sharing)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Elk-Server(YML) file may be used to install only certain pieces of it, such as Filebeat.

![Pentest](Ansible/Pentest(YML).docx)
![Filebeat](Ansible/Filebeat(YML).docx)
![Elk-Server](Ansible/Elk-Server(YML).docx)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting access to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
A jump box is a secure computer that all admins first connect to before launching any administrative task or use as an origination point to connect to other servers or untrusted environments.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the virtual network and system data.
- _TODO: What does Filebeat watch for?_  Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- _TODO: What does Metricbeat record?_ Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name        | Function  | IP Address    | Operating System |
|-------------|-----------|---------------|------------------|
| Jump-Box-VM | Gateway   | 40.88.133.102 | Ubuntu           |
| Web-1       |           | 10.0.0.5      | Ubuntu           |
| Web-2       |           | 10.0.0.7      | Ubuntu           |
| Web-3       |           | 10.0.0.8      | Ubuntu           |
| Elk-Server  | ELK Stack | 40.88.15.108  | Ubuntu           |
|             |           |               |                  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box VM machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_
10.0.0.5 ansible_python_interpreter=/usr/bin/python3
10.0.0.7 ansible_python_interpreter=/usr/bin/python3
10.0.0.8 ansible_python_interpreter=/usr/bin/python3


Machines within the network can only be accessed by using docker to start and then attach the ansible container. Then you have to SSH into it.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_ The Jump-Box. It's IP is 
40.88.133.102
A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 10.0.0.5 10.0.0.7    |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_ it automates the process, just in case you have to install ansible on multiple VMs. This of course makes it faster and more difficult to mess something up.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Configure Elk VM with Docker. It's pretty self-explanatory. All it does is install docker on your ELK Stack so that you can start and attach containers to it
- Use more memory. For some reason, this is required in order to have an ELK installation at all. You will run into problems with your playbook if you dont allocate more memory to it.
-Install pip3. This is just so the ELK installation can read and write python.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Run sudo docker ps
RedAdmin@ELK-Server:~$ sudo docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                                                              NAMES
842caa422ed8        sebp/elk            "/usr/local/bin/star…"   3 hours ago         Up 3 hours          0.0.0.0:5044->5044/tcp, 0.0.0.0:5601->5601/tcp, 0.0.0.0:9200->9200/tcp, 9300/tcp   elk
RysAdmin@ELK-Server:~$

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
10.0.0.5 
10.0.0.7 
10.0.0.8

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

Filebeat logs data involving files on the VM that are not part of the OS
Metricbeat logs various stats regarding the OS and its files.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the id-rsa.pub file to Azure
- Update the hosts file to include IPs of the various VMs that you want to use the playbook on.
- Run the playbook, and navigate to wny one of your VMs to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_ I made multiple playbooks throughout this project. the one I used most was the one labled Pentest. and it was written in YAML after I nano'd into it.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ You update the hosts file and enter whatever IP address you want into it, making sure it's in the right group.
- _Which URL do you navigate to in order to check that the ELK server is running? http://www.dvwa.co.uk/

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
