# ANSIBLE

<img src ="https://ih1.redbubble.net/image.919262417.3645/fposter,small,wall_texture,square_product,600x600.jpg">

## TABLE OF CONTENT
- [INTRODUCTION](#INTRODUCTION) (Parichay)
- [HOW ANSIBLE WORKS ?](#HOW-ANSIBLE-WORKS) (Ye kaam kaise karta hai?)
- [INSTALLATION](#installation) (Sansthapan)
- [GETTING STARTED](#getting-started) (Chaliye shuru karte hai)
- [PLAYBOOKS](#playbooks) (Instructions ki List)
- [INVENTORY](#inventory) (Hosts ki List)
- [VARIABLES](#variables) (Badalne wali cheezein)
- [MODULES](#modules) (Chote-Chote Pre defined programs)
- [ADVANTAGES AND DISADVANTAGES](#advantages-and-disadvantages) (Fayde aur Nuksan)
- [ANSIBLE PLAYBOOK](#ansible-playbook-test-ansible-connection) (Ansible ki instructions ki list)
## INTRODUCTION (Parichay)
**"Ansible"**  word 1966 ki novel *Rocannon's World* by Ursula K. Le Guin se aaya hai. Ye word "Answerable" ka short form h.


Ansible ek open-source tool hai jo configuration management, application deployment, aur task automation jaise kaam ko simplify karta hai. Iska sabse badha feature ye hai ki ye agentless hai, matlab Ansible ko manage karne ke liye kisi software ko nodes pe install karne ki zaroorat nahi hoti.


Jo resources manage karni hoti hain (jaise hosts), unka detail ek file mein hota hai jise **Ansible Inventory** kehte hain.

Aur jo instructions aapko hosts pe run karni hoti hain, wo ek YAML file mein hoti hain, jise **Playbooks** kehte hain.

Jab ek Playbook run hota hai, to host systems se connection banaya jaata hai aur Playbook ki instructions hosts par execute hoti hain.



### USE CASES (Upyog)

- Infrastructure as Code (IaC)
- Continuous Delivery and Continuous Integration (CI/CD)
- Cloud Provisioning
- Configuration Management
- Application Deployment

## HOW ANSIBLE WORKS ? (Ye kaam kaise karta hai?)

Ansible mein **Controller** woh machine hoti hai jaha se aap Ansible commands ya Playbooks run karte ho.


Ansible **Controller** ek machine ya server hota hai jo configuration aur software deployment ko manage karta hai dusre machines (Hosts) pe. Controller koi bhi machine ho sakti hai jo Ansible ke requirements ko fulfill karti hai, jaise laptop, desktop ya virtual machine.

Ansible mein **Host** woh machine hoti hai jise Ansible manage karta hai, yeh physical server ho sakti hai ya virtual machine.
## INSTALLATION (Sansthapan)
Ansible ko install karne ke liye aap package managers ka use kar sakte hain, jaise `apt` Debian/Ubuntu ke liye aur `yum` RedHat ke liye.

### Commands for Installing Ansible (Ansible ko Install karne k liye commands)

Neeche diya huya command latest package information ko fetch karega aur ensure karega ki aapke paas latest versions aur dependencies ho:

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

Niche diya command `software-properties-common` package ko install karega. Is package mein kuch utilities hoti hain jo aapke system ki software sources aur repositories ko manage karna asaan banati hain:



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

Niche diya command Ansible PPA (Personal Package Archive) ko aapke system ki software sources list mein add karega. Isse aapko Ansible ka updated version install karne mein asaani hoti hai:

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

## GETTING STARTED (Chaliye shuru karte h)
### Basic commands
### `ansible`
**Apne managed nodes pe ad-hoc commands run karne k liye.**  
`ansible` command se aap single tasks (known as ad-hoc commands) directly apne managed nodes pe run kar sakte ho bina playbook ke zarurat ke. Yeh useful hota hai jab aap quick troubleshooting ya one-time task kar rahe ho.



For Example,agar apko sabhi hosts pe ping command run karna hai:
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

Ansible current directory ya /etc/ansible/ mein ansible.cfg file dhundta hai. Is file ka use karke tum various configuration options set kar sakte ho.

## PLAYBOOKS (Instructions ki List)

### Playbook Introduction
Playbook wo files hoti h jisme ansible code likha jata h. Playbooks Ansible k saare use cases ka base hoti h. 

### Playbook Structure
- **Hosts:** Wo hosts ki list jinke against playbook run hoga.
- **Tasks:** Actions ki list jo perform karwane h.
- **Handlers:** Tasks k complete hone p additional actions ko trigger karte h.

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

  ## INVENTORY (Hosts ki list)

### Introduction to Inventory
Inventory files m define hota hai ki konse hosts aur group of hosts ko Ansible manage karega.

### Static Inventory
```A simple hosts file:

[webservers]

192.168.1.100

192.168.1.101

[databases]

db.example.com
```

### Host and Group Variables
Tum inventory file mein kisi specific host ya group k liye variables define kar sakte ho.

## VARIABLES (Badalne wali cheezein)

Ansible mein, variables values ko store karne ke liye use hoti hain jo playbooks, roles, aur tasks mein baar-baar use ki ja sakti hain. Yeh playbooks ko zyada dynamic aur flexible banane mein madad karti hain.



## MODULES (Chote-Chote Predefined programs)

## MODULES IN ANSIBLE

Ansible modules bht zaruri caomponents hote h jo tasks perform karte h. Yeh chote programs hote h jo specific tasks karte h jaise package install karna h, file copy karna, ya service ko manage karna. Modules remote hosts p control machine k through execute hote h aur system k different features ko manage karte h.

## ADVANTAGES AND DISADVANTAGES (Fayde aur Nuksan)

## Advantages (Fayde)
- **Agentless:** Managed nodes p koi agent install karne ki zaroorat nahi hoti; sir ssh use hota h.
- **Ease of Use:** Simple Yaml syntax se kaafi asani hoti h.
- **Scalable:** Bht saare servers ko effectively handle karta h.
- **Idempotent:** Baar Baar chalane par bhi results change ni hote.
- **Extensible:** Custom modules aur plugins ko support karta h.
- **Integration:** Dusre tools aur platforms k saath acha kaam karta h.
- **Declarative:** Systems k desired state ko define karta h.
- **Strong Community:** Large ecosystem aur Ansible Galaxy k through support karta h.

## Disadvantages (Nuksan)
- **Performance:** Bht large environments m limitations a skti h.
- **No State Management:** Built-in state tracking nahi hota nodes k liye.
- **Complexity:** Advanced scenarios ko manage karna mushkil ho jata h.
- **Limited Windows Support:** Windows k liye acha support nahi h.
- **No GUI:** Command k line through operate hota h.
- **Advanced Learning Curve:** Complex feautures ko master karna challenging ho sakta h.

# Ansible Playbook: Test Ansible Connection

Ye simple Ansible playbook check karta h ki Ansible sahi se kaam kar raha h ya nahi, agar kaam karta h to ek confirmation message print karega. Playbook ek specified hosts ya group of hosts se connect hota h aur successful execution p message print karta h.

## Playbook: `test_ansible.yml`

```yaml
---
- name: Test Ansible connection
  hosts: all   # 'all' ko specific host ya group se replace kar sakte ho agar zarurat ho
  gather_facts: yes

  tasks:
    - name: Print a message
      debug:
        msg: "Ansible is working!"
```

### Explanation (Vistaar):-
- "name: Test Ansible Connection": Playbook ka ek descriptive name hai.
- "hosts: all": Target hosts ko specify karta h. aap 'all' ko specific group ya hostname se replace kar sakte ho jo inventroy m define h.
- "gather_facts: yes": Ansible target system(s) ke baare m information gather karega,jaise IP addresses, OS type, aur zyada.
- "tasks:": Tasks ki list jo target hosts p execute hongi.
- "name: Print a message:" Task ka description deta h.
- "debug:": Ek module h jo apko output m messages ya variables print karne deta h. 
- msg: "Ansible is working!": Message jo print hoga agar playbook successfully run hota h.














