Ansible stuff for crypta graph.
Right now only distributes secrets from secdist to storm and manp machines (see roles/common/tasks/main.yml)
This is how you run it:
```
./run-ansible.sh [host_or_group]
```

See `hosts` for available hosts and groups.
