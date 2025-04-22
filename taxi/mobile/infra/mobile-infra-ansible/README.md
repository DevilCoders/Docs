Ansible config for mobile build agents
-------

### Configure Host machine

### Mac OS

----

##### Ansible
* `brew install ansible`
##### Sshpass
* `brew install hudochenkov/sshpass/sshpass`

### Ubuntu

----

##### Ansible
* `sudo apt update`
* `sudo apt install software-properties-common`
* `sudo add-apt-repository --yes --update ppa:ansible/ansible`
* `sudo apt install ansible`

##### Sshpass
* `apt-get install sshpass`

### Configure project

----
* `ansible-galaxy install -r requirements.yml` (install requirements for ansible config)
* add passwords for users to .buildagent_pass, .robot_pass, .teamcity_pass