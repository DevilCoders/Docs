
server: https://proxy.sandbox.yandex-team.ru/1331512479
worker: https://proxy.sandbox.yandex-team.ru/1331519546


### prepare:
`ansible-playbook -i hosts.txt prepare.yaml`

### buildfarm server
`ansible-playbook -i hosts.txt playbook-server.yaml`

### buildfarm worker
`ansible-playbook -i hosts.txt playbook-worker.yaml`
