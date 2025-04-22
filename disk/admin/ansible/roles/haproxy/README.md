HAProxy configs
============

###How to add a new Virtual Service
All VSs are described into ```vars/main.yml```.  
Let's look at the example:
```
vs:
  picapica_api:
    name: "picapica_api"
    vs_port: "35023" # Virtual Service's port
    rs_port: "35020" # Real Server's port
    rs_groups: "vertis_vishard-stable" # conductor groups where lives our service
    template: "http-roundrobin.j2"
    dest: "{{ dest_path }}/picapica_api.cfg"
```
After describing VS let's have a look how to assign our VS to the group where clients are located:
```
haproxy_configs:
  vertis_realty_shard_stable: # group name is used like a variable threfore try to avoid symbol "-"
    - "{{ vs.picapica_api }}"
```
Let's create a playbook:
```
> cat haproxy-configure.yml
---

# extra variables:
#   host - requred

- name: Configure HAProxy
  gather_facts: False
  hosts: '{{ host }}'

  roles:
  - role: haproxy
```
And run the playbook against the group or a member of the group ```vertis_realty-shard-stable```:
```
> ansible-playbook -s haproxy-configure.yml -e host=vertis_realty-shard-stable
```
