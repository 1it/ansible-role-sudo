# Ansible role sudoers

This role allows simple management of sudoers

Requirements
------------
* Ansible 2.3.0

Install
------------
`ansible-galaxy install 1it.sudo`

## Variables
Sudoers cmnd alias specification example
```yaml
sudo_nopasswd_group: 'admin' # By default - a group must be created in advance
sudo_set_custom_commands: yes # When not defined a basic config will be set (from templates/etc_sudoers)
sudo_commands_services:
    - /usr/sbin/service nginx reload
    - /usr/sbin/service elasticsearch restart
    - /usr/sbin/service redis-server restart
sudo_commands_main:
    - /sbin/iptables
    - /bin/netstat
    - /usr/bin/supervisorctl
sudo_commands_misc:
    - /usr/sbin/php5dismod
    - /usr/sbin/php5enmod
sudo_custom_definitions:
    - user ALL=(ALL) NOPASSWD: /usr/sbin/nginx
    - editor ALL=(www-data) NOPASSWD: /usr/bin/vim
sudo_set_per_user: # Creates sudoes file in /etc/sudoers.d/user_name with NOPASSWD: ALL directive.
    - alice
    - bob
```
## Playbook example
```yaml
---
- hosts: all
  roles:
    - 1it.sudo
```
