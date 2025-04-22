## yandex-disk-ansible-juggler

### Useful links:

- [Juggler](https://juggler.yandex-team.ru) ([How to get Oauth token](https://docs.yandex-team.ru/juggler/authentication#project-access), or just use [direct link](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=cd178dcdc31a4ed79f42467f2d89b0d0))
- [Disk/Admin/ansible-juggler](https://wiki.yandex-team.ru/disk/admin/ansible-juggler/)
- [common ansible-juggler wiki](https://wiki.yandex-team.ru/sm/juggler/ansible/)
- [Teamcity Build](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Disk_Admin_AnsibleJuggler)

### Auth

Grab Oauth token from juggler and save it to `JUGGLER_OAUTH_TOKEN` environment variable.

### How to add a new cluster
##### 1. Go to project playbook (disk.yml or video.yml)
##### 2. Apply role cluster with vars
```
- role: cluster
  host: <new_cluster>
  tags:
    - disk
    - cluster
    - <new_cluster>
```
##### 3. Test ansible-playbook against your playbook:
```bash
ansible-playbook disk.yml -vv --check --tags <new_cluster>
```
##### 4. Run ansible-playbook against your playbook:
```bash
ansible-playbook disk.yml -vv --tags <new_cluster>
```
 
### How to add a new qloud app
##### 1. Open qloud.yml playbook
##### 2. Assign new role: qloud with arguments
```json
- role: qloud
  tags:
    - qloud
    - <qloud_app name>
  qloud_app: "<qloud_app name>"
  env:
    - name: <qloud_env>
      components:
        - name: "<qloud_component_name>"
        ...
    ...
    - name: testing
      no_report: True
      components:
        - name: "<qloud_component_name>"
```
##### 3. Describe custom checks if needed
In qloud one can define separate checks for environments, but same check for all components (modify if needed).
All other settings same as in clusters.
Example:
```json
- role: qloud
  tags:
    - qloud
    - disk-uploader
  qloud_app: "disk-uploader"
  env:
    - name: stable
      components:
        - name: "uploader"
      checks:
        - name: esets
        - name: esets-bases-data
        - name: esets-key-data
```
##### 4. Run ansible-playbook against your app:
```bash
ansible-playbook qloud.yml -vv [--check] --tags <qloud_app_name>
```

#### Tags in qloud
Tags are added automaticaly:
- "{{ qloud_platform }}.{{ qloud_project }}"
- "{{ qloud_platform }}.{{ qloud_project }}.{{ qloud_app }}"
- "{{ qloud_platform }}.{{ qloud_project }}.{{ qloud_app }}.{{ qloud_env }}"

So Qloud knows about these checks and shows them at the web interface.

### How to add a new balancer
##### 1. Go to balancers.yml playbook
##### 2. Add new role definition
```json
- role: balancer
  host: example.com
  slb_all_default: True
  tags:
    - balancers
    - example.com
```
##### 4. Run ansible-playbook check against your balancer:
```bash
ansible-playbook balancers.yml -vv --check --tags example.com
```
#### 5. Run without --check, for your tag

### Notifications
Notifications are added automaticaly for each responsible person from group_vars/all

## ansible-juggler2

Now it's time to use ansible 2.x+ with ansible-juggler2! Here is a small howTo describing installation and usage with virtualenv (suggested by [developers](https://wiki.yandex-team.ru/sm/juggler/ansible/#ansible2)).

Sample usage:

```bash
$ virtualenv venv
# or
$ mkvirtualenv venv

# change it
$ source venv/bin/activate
# or
$ workon venv
$ which ansible-playbook # == ~/.virtualenvs/venv/bin/ansible-playbook

# install deps
$ pip install --index-url https://pypi.yandex-team.ru/simple/ ansible ansible-juggler2

# get updates
$ pip install --index-url https://pypi.yandex-team.ru/simple/ ansible ansible-juggler2 --upgrade

# apply playbook
$ ./venv/bin/ansible-playbook my-playbook.yml
# or
$ ansible-playbook my-playbook.yml

# exit from env
$ deactivate
```
