Moved from https://github.yandex-team.ru/CRM/teamcity-agent-docker-frontend

Adapted for Ya.Deploy and Qloud

## Build
ya package --docker --docker-push --target-platform linux --docker-repository crm --docker-network=host package.json
