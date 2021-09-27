OpenWRT Config DDNS
=========

[![Role](https://img.shields.io/ansible/role/56374.svg)](https://galaxy.ansible.com/pe_pe/openwrt_config_ddns/)
[![Quality](https://img.shields.io/ansible/quality/56374.svg)](https://galaxy.ansible.com/pe_pe/openwrt_config_ddns/)
[![CI](https://github.com/pe-pe/ansible_role_openwrt_config_ddns/workflows/CI/badge.svg)](https://github.com/pe-pe/ansible_role_openwrt_config_ddns/actions)

Ansible role that configures ddns settings of OpenWRT device (mainly those which are usually defined in `/etc/config/ddns`).

Requirements
------------
None

Role variables
--------------
Configuration settings defined in `openwrt_config_ddns` variable which are to be applied on OpenWRT device.
```yaml
openwrt_config_ddns:
  ddnssvc: { service_name: testsvc, username: testuser, password: testpass, domain: test.lan, lookup_host: test.lan,
             ip_source: web, ip_url: http://testip.internet, interface: test, ip_network: wan, enabled: 0 }
```
If `openwrt_config_ddns` configuration variable is not present - no changes are made by role.

Dependencies
------------
This role depends on Ansible role `gekmihesg.openwrt` which allows to manage OpenWRT and derivatives with Ansible but without Python.

Example playbook using the role
-------------------------------
`./host_vars` \
`./host_vars/myrouter.yml`
```yaml
---
openwrt_config_ddns:
  ddnssvc: { service_name: testsvc, username: testuser, password: testpass, domain: test.lan, lookup_host: test.lan,
             ip_source: web, ip_url: http://testip.internet, interface: test, ip_network: wan, enabled: 0 }
```
`./inventory.ini`
```ini
[openwrt]
myrouter
```
`./roles` \
`./roles/requirements.yml`
```yaml
---
roles:
- name: gekmihesg.openwrt
- name: pe_pe.openwrt_config_ddns
```
`./site.yml`
```yaml
---
- hosts: all
  roles:
    - role: gekmihesg.openwrt
    - role: pe_pe.openwrt_config_ddns
```
`./ansible.cfg`
```ini
[defaults]
# Define inventory location
inventory = ./inventory.ini
# Where to put roles downloaded from galaxy and other repos
roles_path = ./roles
# Defaults to /tmp to avoid flash wear on target device
remote_tmp = /tmp
```

Example execution
-----------------
Install roles and requirements:
```
ansible-galaxy role install -r roles/requirements.yml
```
Preview changes execution would perform on inventory:
```
ansible-playbook site.yml --check --diff
```
Execute playbook on inventory:
```
ansible-playbook site.yml
```
License
-------
MIT

Author Information
------------------
PePe
