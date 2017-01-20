# ansible-dcos
Ansible playbook for dc/os

# This playbook can be used for AWS as well as on-premises.
For more info: Check [here](https://www.vishnu-tech.com/blog/ansible-dcos/)

# Variables
* Check Vars folder

```
centos_ami: ami-0389a870
aws_region: eu-west-1
aws_vpc_subnet_id: subnet-xxxx
private_domain: example.com
aws_key_name: awskeypair
instance_zone: b
instance_type: t2.large
instance_sg_id: sg-xxxx
instance_sg_id_dcos_master: sg-xxx
instance_sg_id_dcos_slave: sg-xxx
instance_profile: "dcos"
instance_role_bs: dcos-bs
instance_role_master: dcos-master
instance_role_slave: dcos-slave
aws_env: development

```

# Executing playbook in aws

```
For dcos bootstrap server:
==========================
ansible-playbook playbook/dcos-bs.yml --private-key <path to your aws key>

For dcos master server:
=======================
ansible-playbook playbook/dcos-master.yml --private-key <path to your aws key>

For dcos slaves server:
=======================
ansible-playbook playbook/dcos-slaves.yml --private-key <path to your aws key>

For dcos deploy:
================

ansible-playbook playbook/dcos-setup.yml --private-key <path to your aws key>

```

To run in on-premises, remove the aws parts in the playbook & use it as below. Also alter the inventories according to your on-premise setup

```
Example: For bootstrap node
===========================

- name: Configured instances
  hosts: dcos-bs
  gather_facts: true
  become: yes
  become_user: root
  vars:
    instance_role: dcos-bs
  pre_tasks:
    - include_vars: ../vars/common.yml
  roles:
    - common
```    
