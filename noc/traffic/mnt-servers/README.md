# Description

Package contains files and scripts for mnt servers, where lives l3-manager and dns-manager.  
It also contains different configs for setup and manage l3balancers.

# Build

    ya package --debian --key=XXX mnt-servers/focal.json
    ya package --debian --key=XXX mnt-servers/trusty.json

# First setup

Package doesn't contains private data, you should deploy/copy it by yourself:

- .pem certificates and keys
- OAuth data for proxy_pass
- l3manager security environment
- sources.list for chosen distrib, eg "focal"

        deb http://mnt-traf.dist.yandex.ru/mnt-traf stable/all/
        deb http://mnt-traf.dist.yandex.ru/mnt-traf stable/amd64/
        deb http://mnt-traf-focal.dist.yandex.ru/mnt-traf-focal stable/all/
        deb http://mnt-traf-focal.dist.yandex.ru/mnt-traf-focal stable/amd64/

Additional manual actions:

- install docker

        sudo apt install docker.io

        # repository contains old docker-compose, get it from github.com
        sudo curl -L "https://github.com/docker/compose/releases/download/1.28.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
        sudo chmod 755 /usr/local/bin/docker-compose

- update ttmgmt UID and GID

        sudo usermod -u 1234 ttmgmt
        sudo groupmod -g 1234 ttmgmt
