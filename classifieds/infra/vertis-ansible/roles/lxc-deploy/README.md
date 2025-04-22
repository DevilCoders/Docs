ansible-role-lxc-deploy
======================

Ansible role that helps to create LXC container  

####Follow next steps to create VM (you should use conductor):

1. Describe host on conductor
2. Create playbook and run it (see example #1)

example #1
```
---
# lxc-deploy.yml
# extra variables:
#   host - required
#   container - required

- name: Create LXC container
  gather_facts: false
  hosts: '{{ host }}'

  roles:
  - role: lxc-deploy
    container_name: '{{ container }}'
```
