
Install Guide - https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
* The only officially supported installation method is by using Python's PIP package manager
* Ansible is not oficially supported on Windows (as a control node)

Ansible Porting Guide: https://docs.ansible.com/ansible/latest/porting_guides/porting_guides.html
- Used to help upgrade version of Ansible

`ansible-doc -t connection -l` or `ansible-doc --type connection --list`
- Command that's helpful to learn on the fly about Ansible capabilities. This particular command looks at all "connection" plugins that are available.



## Basics
- Ansible uses SSH to control hosts
- No software is required on managed nodes
- An Ansible **inventory** is a list of managed nodes that is logically organized for Assible to manage.

