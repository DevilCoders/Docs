# Install l3manager agent

# How to run
```
cd noc/traffic/mnt-servers/confs/ansible/playbooks/roles/l3manager_agent
cat inventory.ini
[l3agents]
iva-lb36a-25d.yndx.net
ansible-playbook -i inventory.ini ../../l3-agent-setup.yml --check --diff -el3_manager_agent_version='=2.0.14'
```

# TODO
Create generator for inventory and parameters.
```
./gen_inventory <LB_group> <agent_version> <agent_config> <whatever_paraemeters>  > inventory.yml
ansible-playbook -i inventory.yml agent_deploy.yml
```
