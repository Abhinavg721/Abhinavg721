# ANSIBLE

<img src ="https://ih1.redbubble.net/image.919262417.3645/fposter,small,wall_texture,square_product,600x600.jpg">

## TABLE OF CONTENT
- [INTRODUCTION](#INTRODUCTION)
- [HOW ANSIBLE WORKS ?](#HOW-ANSIBLE-WORKS)
- [INSTALLATION](#installation)
- [GETTING STARTED](#getting-started)
- [PLAYBOOKS](#playbooks)
- [INVENTORY](#inventory)
- [VARIABLES](#variables)
- [MODULES](#modules)
- [ADVANTAGES AND DISADVANTAGES](#advantages-and-disadvantages)
- [ANSIBLE PLAYBOOK](#ansible-playbook-test-ansible-connection)
## INTRODUCTION
The word **"Ansible"**  came from the 1966 novel *Rocannon's World* by Ursula K. Le Guin. The word was a contraction of "Answerable".


Ansible is an open-source tool that simplifies tasks such as configuration management, application deployment, and task automation. It is agentless, meaning it doesn't require any software to be installed on the managed nodes.


The details about the resources to manage (hosts) are kept in a file called the **Ansible Inventory**.

The instructions to run on hosts are kept in a YAML file called **Playbooks**.

When a Playbook is run, a connection is made to the host systems, and the Playbook instructions are executed on the hosts.



### USE CASES

- Infrastructure as Code (IaC)
- Continuous Delivery and Continuous Integration (CI/CD)
- Cloud Provisioning
- Configuration Management
- Application Deployment

## HOW ANSIBLE WORKS ?

In Ansible, the **Controller** is the machine where you run Ansible commands or Playbooks.


Ansible **Controller** is the machine or server that manages the configuration and deployment of software to other machines (Hosts). The controller can be any machine that meets the requirements for running Ansible, such as a laptop, a desktop computer, or a virtual machine.

Ansible "**Host**" is any machine that Ansible is managing, this can be a physical server or a virtual machine.
## INSTALLATION
Ansible can be installed using package managers like `apt` for Debian/Ubuntu and `yum` for RedHat.

### Commands for Installing Ansible

The following command will fetch updated package information, ensure access to the latest versions, and resolve dependencies:

```bash
sudo apt-get update
```
### Output:-
```
W: Failed to fetch http://in.archive.ubuntu.com/ubuntu/dists/jammy-backports/InRelease  Temporary failure resolving 'in.archive.ubuntu.com'
W: Failed to fetch http://security.ubuntu.com/ubuntu/dists/jammy-security/InRelease  Temporary failure resolving 'security.ubuntu.com'
W: Failed to fetch https://packages.microsoft.com/repos/vscode/dists/stable/InRelease  Temporary failure resolving 'packages.microsoft.com'
W: Failed to fetch https://download.docker.com/linux/ubuntu/dists/jammy/InRelease  Temporary failure resolving 'download.docker.com'
W: Failed to fetch https://packages.microsoft.com/repos/code/dists/stable/InRelease  Temporary failure resolving 'packages.microsoft.com'
W: Some index files failed to download. They have been ignored, or old ones used instead.
```

The following command will install the `software-properties-common` package on your system. This package includes a set of utilities that make it easier to manage your system's software sources and repositories:

```bash
sudo apt-get install software-properties-common
```
### Output:-
```
/$ sudo apt-get install software-properties-common
[sudo] password for abhinav: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
software-properties-common is already the newest version (0.99.22.9).
0 upgraded, 0 newly installed, 0 to remove and 23 not upgraded.
```

The following command will add the Ansible PPA (Personal Package Archive) to your system's list of software sources. This allows you to install and update Ansible directly from this PPA, which often contains more up-to-date versions of Ansible than the default repositories:

```bash
sudo add-apt-repository ppa:ansible/ansible
```
```abhinav@gautam:/$ sudo add-apt-repository ppa:ansible/ansible
Repository: 'deb https://ppa.launchpadcontent.net/ansible/ansible/ubuntu/ jammy main'
Description:
Ansible is a radically simple IT automation platform that makes your applications and systems easier to deploy. Avoid writing scripts or custom code to deploy and update your applications— automate in a language that approaches plain English, using SSH, with no agents to install on remote systems.

http://ansible.com/

If you face any issues while installing Ansible PPA, file an issue here:
https://github.com/ansible-community/ppa/issues
More info: https://launchpad.net/~ansible/+archive/ubuntu/ansible
Adding repository.
Press [ENTER] to continue or Ctrl-c to cancel. 
Adding deb entry to /etc/apt/sources.list.d/ansible-ubuntu-ansible-jammy.list
Adding disabled deb-src entry to /etc/apt/sources.list.d/ansible-ubuntu-ansible-jammy.list
Adding key to /etc/apt/trusted.gpg.d/ansible-ubuntu-ansible.gpg with fingerprint 6125E2A8C77F2818FB7BD15B93C4A3FD7BB9C367
Hit:1 https://download.docker.com/linux/ubuntu jammy InRelease
Hit:2 http://in.archive.ubuntu.com/ubuntu jammy InRelease                                           
Get:3 https://packages.microsoft.com/repos/vscode stable InRelease [3,594 B]                        
Hit:4 https://dl.google.com/linux/chrome/deb stable InRelease                                       
Hit:5 https://packages.microsoft.com/repos/code stable InRelease                                    
Get:6 http://in.archive.ubuntu.com/ubuntu jammy-updates InRelease [128 kB]                
Get:7 http://security.ubuntu.com/ubuntu jammy-security InRelease [129 kB]      
Get:8 https://packages.microsoft.com/repos/vscode stable/main amd64 Packages [26.4 kB]              
Get:9 https://ppa.launchpadcontent.net/ansible/ansible/ubuntu jammy InRelease [18.0 kB]             
Get:10 https://ppa.launchpadcontent.net/ansible/ansible/ubuntu jammy/main i386 Packages [1,116 B]   
Hit:11 http://in.archive.ubuntu.com/ubuntu jammy-backports InRelease                        
Get:12 https://ppa.launchpadcontent.net/ansible/ansible/ubuntu jammy/main amd64 Packages [1,116 B]
Get:13 https://ppa.launchpadcontent.net/ansible/ansible/ubuntu jammy/main Translation-en [752 B]    
Get:14 http://in.archive.ubuntu.com/ubuntu jammy-updates/main i386 Packages [690 kB]          
Get:15 http://in.archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages [1,987 kB]
Fetched 2,985 kB in 4s (813 kB/s)                            
Reading package lists... Done
```

## GETTING STARTED
### Basic commands
### `ansible`
**Run ad-hoc commands on your managed nodes.**  
The `ansible` command allows you to run single tasks (known as ad-hoc commands) directly on your managed nodes without the need for a playbook. This is useful for quick, one-off tasks or troubleshooting.

For example, to ping all hosts in your inventory:
```bash
ansible all -m ping
```
### Output:-
```
abhinav@gautam:/$ ansible all -m ping
lakshmi | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```
### Ansible Configuration File

Ansible looks for the `ansible.cfg` file in the current directory or `/etc/ansible/`. This file can be used to set various configuration options.

## PLAYBOOKS

### Introduction to Playbooks
Playbooks are the files where the ansible code is writtenand it is in YML format. These files are basically the building blocks for all the use cases of Ansible. 

### Playbook Structure
- **Hosts:** The group of hosts the playbook will run against.
- **Tasks:** A list of actions to perform.
- **Handlers:** Triggered by tasks to perform additional actions.

```
PLAYBOOK STRUCTURE

---

- Hosts:  
  List of hosts

- Variables:  
  Variables are used to make your playbooks dynamic

- Tasks:  
  Name of tasks

- Handlers:  
  Handlers are triggered by the `notify` directive.  
  They are used for actions like restarting a service.
  ```

  ## INVENTORY

### Introduction to Inventory
Inventory files define the hosts and groups of hosts that Ansible manages.

### Static Inventory
```A simple hosts file:

[webservers]

192.168.1.100

192.168.1.101

[databases]

db.example.com
```

### Host and Group Variables
You can define variables specific to a host or a group in the inventory file.

## VARIABLES

In Ansible, variables are used to store values that can be reused throughout playbooks, roles, and tasks. They help make your playbooks more dynamic and flexible. Here’s a breakdown of how variables work in Ansible.

## MODULES

## MODULES IN ANSIBLE

Ansible modules are the core components used to perform tasks in Ansible. They are small programs that perform a specific task such as installing a package, copying a file, or managing a service. Modules are executed on remote hosts by the Ansible control machine and can manage various aspects of a system.

## ADVANTAGES AND DISADVANTAGES

## Advantages
- **Agentless:** No need to install agents on managed nodes; uses SSH.
- **Ease of Use:** Simple YAML syntax; minimal learning curve.
- **Scalable:** Handles large numbers of servers effectively.
- **Idempotent:** Ensures consistent results with repeated runs.
- **Extensible:** Supports custom modules and plugins.
- **Integration:** Works well with other tools and platforms.
- **Declarative:** Defines desired state of systems.
- **Strong Community:** Large ecosystem and support through Ansible Galaxy.

## Disadvantages
- **Performance:** May face limitations in extremely large environments.
- **No State Management:** Lacks built-in state tracking for nodes.
- **Complexity:** Advanced scenarios can be hard to manage.
- **Limited Windows Support:** Less mature support for Windows.
- **No GUI:** Operates primarily via the command line.
- **Advanced Learning Curve:** Mastering complex features can be challenging.

# Ansible Playbook: Test Ansible Connection

This simple Ansible playbook checks if Ansible is working by printing a confirmation message. The playbook connects to a specified host or group of hosts and outputs a message to indicate successful execution.

## Playbook: `test_ansible.yml`

```yaml
---
- name: Test Ansible connection
  hosts: all   # Replace 'all' with a specific host or group if needed
  gather_facts: yes

  tasks:
    - name: Print a message
      debug:
        msg: "Ansible is working!"
```

### Explanation:-
- "name: Test Ansible Connection": A descriptive name for the playbook.
- "hosts: all": Specifies the target hosts.you ca n replace 'all' with a specific group or hostname defined in your inventory.
- "gather_facts: yes": Ansible will gather about the target systems(s), which include information like IP adresses, OS type, and more.
- "tasks:": The list of tasks that will be exevuted on the target hosts.
- "name: Print a message:" Describe the tasks that will run.
- "debug:": A module that allows you to print messages or variables to the output.
- msg: "Ansible is working!": The message that will be printed if the playbook runs successfully.














