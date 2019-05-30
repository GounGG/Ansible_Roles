Role Name
=========

ElasticSearch 5.5.3 Install,Higher versions can also be installed, but without testing。

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

# Host Inventory

```shell
[es_master]
master01 ansible_ssh_host=es-sh01-173.int.uops.cn
master02 ansible_ssh_host=es-sh01-172.int.uops.cn
master03 ansible_ssh_host=es-sh01-174.int.uops.cn

[es_data]
data01 ansible_ssh_host=es-sh01-130.int.uops.cn
data02 ansible_ssh_host=es-sh01-129.int.uops.cn
data04 ansible_ssh_host=es-sh01-142.int.uops.cn
data05 ansible_ssh_host=es-sh01-141.int.uops.cn
data06 ansible_ssh_host=es-sh01-128.int.uops.cn
data03 ansible_ssh_host=es-sh01-176.int.uops.cn

[es_client]
client01 ansible_ssh_host=es-sh01-175.int.uops.cn
client02 ansible_ssh_host=es-sh01-134.int.uops.cn

[elastic:children]
es_master
es_data
es_client
```

# Group Variables

group_vars/es_master 

```shell
master: "true"
data: "false"
ingest: "false"
xms: '2g'
xmx: '2g'
```

group_vars/es_data

```shell
---
master: "false"
data: "true"
ingest: "false"
xms: '8g'
xmx: '8g'
```

group_vars/es_client

```shell
---
master: "false"
data: "false"
ingest: "false"
xms: '18g'
xmx: '18g'
```

Role Variables
--------------

vars/main.yml

```yaml
---
# vars file for elasticsearch
data_dir: '/data/sysadmin/service_run_data/es_data01,/data/sysadmin/service_run_data/es_data02,/data/sysadmin/service_run_data/es_data03'
log_dir: '/var/log/es_log'
listen_ip: '0.0.0.0'
listen_port: '9200'
cluster_name: 'ulucu'
```

Handlers
------------

```yaml
---
# handlers file for elasticsearch
- name: Restart es server
  service:
    name: elasticsearch
    state: restarted
  tags:
    - Restart
```

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
