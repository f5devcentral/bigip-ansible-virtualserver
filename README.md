# bigip-ansible-virtualserver
Ansible role to configure nodes/pools and virtual server on the BIG-IP

This is a workflow to
* Add nodes to the BIG-IP
* Add a pool to the BIG-IP
* Add nodes to the Pool
* Add a virtual server

## Requirements
* This role requires Ansible 2.4
* BIG-IP is licensed
* Packages to be installed
  - pip install f5-sdk
  - pip install bigsuds
  - pip install netaddr

## Role Variables
The variables that can be passed to this role and a brief description about them are as follows.

```
username: "admin"
password: "admin"

pool_name: "web-pool"

vip_name: "http_virtual_server"
vip_port: "80"
vip_ip: "10.168.68.143"

pool_members:
- port: "80"
  host: "192.168.68.160"
- port: "80"
  host: "192.168.68.161"
```

## Example Playbook
```
- hosts: bigip
  gather_facts: false
  roles:
  - { role: f5devcentral.bigip-ansible-virtualserver }

```

## Sample inventory file

```
[bigip]
10.20.30.40
```

## Credential storage

Because this role includes usage of credentials to access your BIG-IP, I recommend that you supply these variables in an ansible-vault encrypted file.

This can be supplied out-of-band of this role

Steps:
- Store your vault password in a file - '~/.vault_pass.txt'
- Execute playbook as follows - ansible-vault encrypt <<variable_filename>> --vault-password-file ~/.vault_pass.txt

For more information refer to: http://docs.ansible.com/ansible/latest/playbooks_vault.html

## Certificate validation
To validate the SSL certificates of the BIG-IP REST API
- set validate_certs: true
- Generate a public private key pair
- Store the public key on BIG-IP (https://support.f5.com/csp/article/K13454#bigipsshdaccept)

## Credits
https://github.com/F5Networks/f5-ansible
