ansible-dynamic-inventory
===

Prepare for usage
---

Save `config.json` as `~/.ansible/dynamic-inventory-config.json` folder or create symlink.

Create ansible config file in `~/.ansible.cfg` by the example:
```
[defaults]

remote_user=root
module_name = shell
command_warnings = True
display_skipped_hosts = False
gathering = smart
host_key_checking = False
forks=10
ansible_user=<YOUR USER>
deprecation_warnings=False

inventory = <PATH TO>/ansible-dynamic-inventory/inventory.py

action_plugins     = plugins/action_plugins
callback_plugins   = plugins/callback_plugins
connection_plugins = plugins/connection_plugins
lookup_plugins     = plugins/lookup_plugins
vars_plugins       = plugins/vars_plugins
filter_plugins     = plugins/filter_plugins

vault_password_file = /Users/<YOUR USER>/vault_password_file

[ssh_connection]
pipelining = True
ssh_args = -o ControlMaster=auto
control_path = %(directory)s/%%h-%%rn
```
Put your username in `ansible_user`, path to the `inventory.py` in `hostfile`, path to the file with vault password in `vault_password_file`.

You could run the following command in the directory `vertis-ansible/` to make sure everything is working:
```
ansible-playbook vertis_vdev_tc.yml --tags autorelease
```

Using in bash auto complete
---
Put following lines in  `.bash_profile` or `.bashrc` file:
```
echo -n "# Refreshing hosts data from Conductor ... " 1>&2
C_HOSTS=$(python ~/Projects/ansible-dynamic-inventory/inventory.py --bash-completion-hosts 2>/dev/null)
H_RESULT=$?
if [ $H_RESULT -eq 0 ]; then
    complete -W "$C_HOSTS" ssh ping ping6
    echo 'done.'
else
    echo 'failed!'
fi
echo -n "# Refreshing groups data from Conductor ... " 1>&2
C_GROUPS=$(python ~/Projects/ansible-dynamic-inventory/inventory.py --bash-completion-groups 2>/dev/null)
G_RESULT=$?
if [ $H_RESULT -eq 0 ] && [ $G_RESULT -eq 0 ]; then
    complete -f "*.yml" -d ansible-playbook
    complete -W "$C_GROUPS $C_HOSTS" ansible
    echo 'done.'
else
    echo 'failed!'
fi
```
Then just refresh bash profile (or open new terminal instead):
```
notebook:~ user$ . .bash_profile
# Refreshing hosts data from Conductor ... done.
notebook:~ user$
```
And then feel free to complete host names by pressing `Tab`!

Another version of auto complete combined with auto complete from `.ssh/known_hosts` and `.ssh/config`.
---
This version have files cache.
Auto update is disabled!
Cache will be updated by call `inventory-update` command manually.

Lines of code for `.bashrc`:
```
# cache for auto complete
cache_dir="${HOME}/.cache"
c_hosts_cache="${cache_dir}/c_hosts_cache.txt"
c_groups_cache="${cache_dir}/c_groups_cache.txt"
[ -d ${cache_dir} ] || mkdir ${cache_dir}

inventory-update()
{
    local _inventory_py _c_hosts _h_result _c_groups _g_result

    _inventory_py="${HOME}/work/ansible-dynamic-inventory/inventory.py"

    echo -n '# Refreshing inventory file ... ' 1>&2
    python ${_inventory_py} --update 2>/dev/null 1>&2
    _i_result=$?
    if [ "${_i_result}" -eq 0 ]; then
        echo 'done.'
    else
        echo 'failed!'
    fi

    echo -n '# Refreshing hosts data from Conductor ... ' 1>&2
    _c_hosts=$(python ${_inventory_py} --bash-completion-hosts 2>/dev/null)
    _h_result=$?
    if [ "${_h_result}" -eq 0 ]; then
        if [ -n "${_c_hosts}" ]; then
            echo ${_c_hosts} > ${c_hosts_cache}
        fi
        echo 'done.'
    else
        echo 'failed!'
    fi

    echo -n '# Refreshing groups data from Conductor ... ' 1>&2
    _c_groups=$(python ${_inventory_py} --bash-completion-groups 2>/dev/null)
    _g_result=$?
    if [ "${_h_result}" -eq 0 ] && [ "${_g_result}" -eq 0 ]; then
        if [ -n "${_c_groups}" ]; then
            echo ${_c_groups} > ${c_groups_cache}
        fi
        echo 'done.'
    else
        echo 'failed!'
    fi

    echo -n '# Updating autocompletes ... ' 1>&2
    _completes
    _u_result=$?
    if [ "${_u_result}" -eq 0 ]; then
        echo 'done.'
    else
        echo 'failed!'
    fi
}

# autocomplete for ssh hostname from known_hosts and config
# https://www.shocm.com/2011/01/ssh-autocomplete-on-osx/
_complete_ssh_hosts()
{
    local _known_hosts _config _comp_ssh_hosts

    COMPREPLY=()
    cur="${COMP_WORDS[COMP_CWORD]}"

    if [ -f ~/.ssh/known_hosts ]; then
        _known_hosts=$(cat ${HOME}/.ssh/known_hosts | \
                       cut -f 1 -d ' ' | \
                       sed -e s/,.*//g | \
                       grep -v ^# | \
                       uniq | \
                       grep -v "\[")
    fi

    if [ -f ~/.ssh/config ]; then
        _config=$(cat ${HOME}/.ssh/config | \
                  grep "^Host " | \
                  sed -e s/*.*//g | \
                  awk '{print $2}')
    fi

    if [ -s "${c_hosts_cache}" ]; then
        c_hosts=$(cat ${c_hosts_cache})
    fi

    _comp_ssh_hosts="${_known_hosts} ${_config} ${c_hosts}"

    COMPREPLY=( $(compgen -W "${_comp_ssh_hosts}" -- $cur))
    return 0
}

_completes()
{
    if [ -s "${c_groups_cache}" ]; then
        c_groups=$(cat ${c_groups_cache})
    fi
    complete -W "${c_groups}" -F _complete_ssh_hosts ansible
    complete -F _complete_ssh_hosts ssh scp ping ping6
}

_completes
```
Just call `inventory-update` for update data:
```
notebook:~ $ inventory-update
# Refreshing inventory file ... done.
# Refreshing hosts data from Conductor ... done.
# Refreshing groups data from Conductor ... done.
# Updating autocompletes ... done.

notebook:~ $
```

Generic examples
---

```
$ ansible-playbook -i inventory.py common.yml -e host=some-host-or-group
$ ansible-playbook -i inventory.py common.yml -e host=all --limit some-host-or-group
```

Script help message
---

```
$ ./inventory.py -h
usage: inventory.py [-h] [--config-file CONFIG_FILE] [--projects PROJECTS]
                    [--api_url API_URL] [--update]

Produce an Ansible Inventory file based on Conductor API info

optional arguments:
  -h, --help            show this help message and exit
  --config-file CONFIG_FILE, -f CONFIG_FILE
                        Use specified config file, must be a valid JSON file
                        (default: ~/.ansible/dynamic-inventory-config.json)
  --projects PROJECTS, -p PROJECTS
                        Specify list of a projects to override config file,
                        comma-separated (default: None, using list from
                        config)
  --api_url API_URL, -a API_URL
                        Override config URL where Conductor API is available
                        (default: None, using value from config)
  --update, -u          Force using most actual info, may be slower that
                        Conductor's cache (default: False)
```
