Initial_Server_Setup
=========

This Ansible role performs the usual steps to prepare a server for hosting apps that are exposed to the public.

Also find it on [ansible galaxy](https://galaxy.ansible.com/jstet/initial_server_setup).


Requirements
----------------
- You must be able to log in via ssh as a user that has sudo privileges.
- Ansible facts must have been gathered.
- You need to "become" for the role to work

Role Variables
--------------
Use the "extra_packages" variable to install additional packages.

Example usage:
```
extra_packages:
  - package_name
```

The variable "firewall" (defaults to true) allows you to decide if you want a firewall to be set up or not.

Example usage:
```
firewall: false
```

To allow ports/protocols through firewall, use the variable "services". "trusted" is optional; if undefined, all IPs are allowed.

Example usage:
```
services:  
  - name: service_name
    port: port_number
    protocols
      - udp
      - tcp
      - icmp
    trusted:
      - IP
      - IP
```
Example Playbook
----------------
```
- hosts: all
  gather_facts: yes
  become: no
  tasks:
    - block:
      - name: Initial server setup (security etc.)
        include_role:
          name: jstet.initial_server_setup
        vars:
          extra_packages:
            - htop
            - net-tools
          services:
            - name: http
              port: 80
              protocols:
                - tcp
                - udp
              trusted:
                - 216.58.190.0
                - 174.23.123.1
            - name: https
              port: 443
              protocols:
                - tcp
                - udp
      become: yes
```
Installation
------------------
```
ansible-galaxy install jstet.initial_server_setup
```
Another option would be to include the role in requirements.yml and then to run:
```
ansible-galaxy install -r requirements.yml
```
