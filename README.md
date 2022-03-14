Initial_Server_Setup
=========

This Ansible performs the usual steps to prepare a server for hosting apps exposed to the public.


Requirements
----------------
- You must be able to log in via ssh as a user that has sudo privileges.
- Ansible facts must have been gathered.
- You need to "become" for thr role to work

Role Variables
--------------
Use the "extra_packages" variable to install additional packages.

extra_packages:
  - package_name

To allow ports/protocols through firewall, use the variable "services". "trusted" is optional; if undefined all IPs are allowed.

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


Example Playbook
----------------
- hosts: all
  gather_facts: yes
  become: no
  tasks:
    - block:
      - name: Initial server setup (security etc.)
        include_role:
          name: jstet.initial_server_setup
        vars:
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


License
-------

MIT

Author Information
------------------

Visit my [homepage](jstet.net)
