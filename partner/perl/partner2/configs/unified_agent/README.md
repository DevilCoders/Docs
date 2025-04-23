### Сборка образа

```
export UNIFIED_AGENT_DOCKER_VERSION=<next_version>
docker build . --tag registry.yandex.net/partners/unified-agent:${UNIFIED_AGENT_DOCKER_VERSION}
docker push registry.yandex.net/partners/unified-agent:${UNIFIED_AGENT_DOCKER_VERSION}
```

### Обновить ресурс в sandbox
Загрузить новую версию командой
```

ya upload --ttl inf configs/unified_agent/config.yaml -T PARTNER_UNIFIED_AGENT_CONFIG
```
и указать ссылку на стейджах в деплое (пример `sbr:2881185261`)

Config -> Services -> Disk, volumes and resources -> UnifiedAgentConf -> Resource URL
