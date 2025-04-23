salt
====

Конфигурации и рецепты salt-a

Клонирование производить в /srv.


Testing
-------

Linux testing is done with ``kitchen-salt``.

1) Install ruby (via rbenv)
https://github.com/saltstack/kitchen-salt/blob/master/docs/gettingstarted.md

2) Install kitchen 
``bundle install``
3) Install docker
4) Suite list
``kitchen list``
5) Run suite
``kitchen converge common-ubuntu-1804``
6) Clean
``kitchen destroy``

Local debugging (after ``converge``)
1) Hack
2) Copy
``docker cp ./salt/components postgresubuntu1404-bpsavelev-bpsavelev-mq2xabe1:/tmp/kitchen/srv/salt/``
3) Run
``kitchen login``
``sudo -E salt-call --state-output=changes --config-dir=/tmp/kitchen/etc/salt state.sls components.common test=True``
