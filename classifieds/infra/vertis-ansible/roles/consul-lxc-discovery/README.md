ansible-role lxc-consul-discovery

======================
Exports lxc hosts from lxcbox to consul

GitHUB https://github.com/YandexClassifieds/consul-lxc-discovery

Usage:

```yaml
  roles:
    - role: lxc-consul-discovery
    - { role: "lxc-consul-discovery", tag_list: "lb,nginx" }
    - { role: "lxc-consul-discovery", when: "'lxcbox-c-' in inventory_hostname", tag_list: "cassandra,databases" }
```
