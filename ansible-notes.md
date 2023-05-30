ansible:
--------
what is ansible?
	ansible is a configuration management tool...
what is configuration management tool?
	it is maintain number(100 and 1000's) of machines with automation

what it maintain ?
	it maintain the system resources such as
	1)install a application
	2)configuration
	3)updates
	4)maintain and so on..

why configuration management tool?
	->reduce management complexity
	->save time

infrastructure as a code:
------------------------
- with the code we can manage the infrastructure
	
configuration management tools?
	puppet ----> 2005	pull
	chef ------->2008	pull
	ansible ----->2011	push
how ansible work?
	ansible is working based on push mechanisam. push based means here server(master) will push the code into the nodes(slaves).

how the master communicate with slaves?
	with ssh public key & private key they communicate.

how to install ansible?
	2 ways to install 
	i)pip install ansible (it is python module)
	ii)yum -y install ansible (before that you can install epel-release "yum -y install epel-release" and enable it)

 - localhost is my master
 - techmine is my node.

- create the master user private & public key 
- then place the master public key in  "authorized_keys" file
- cat id_rsa.pub>>authorized_keys
- then copy key to nodes
- ssh-copy-id root@(nodeip)
- set nodes in master (/etc/ansible/hosts) file

- we can work with ansible in 2 ways
 i)playbooks (all tasks place in one .yml file and run it)
 ii)ad-hoc (on the command line we perform this)

ansible playbooks:
------------------
Q)what is playbook?
	playbook is a set of instructions file. to do a particular tasks on target(host) or group of target(hosts).

Q)how playbook works?
	playbook works with modules(yum,service,file,etc..), and inventory file(/etc/ansible/hosts) over ssh communication.

Q)what we need to run playbook ?
	we need to specify target, tasks in playbook with modules(yum, file, etc..)


Q)how playbook start?

---
- name: sample playbook
  hosts: target host (or) hosts name specified in (/etc/anisble/hosts)
  tasks:
  - name:

1)creation sample file	- file
2)install application (httpd)	- yum
3)start service (httpd)	- service
4)copy file (index.html)	- template


ansible role:
------------
	- place the group of playbooks in one file. it will help reduce the code complexity, and increase the code reusability.



