# Avia solomon-agent sidecar for Deploy

Сборка solomon-agent для использования в Deploy в качестве sidecar.

## Сборка и загрузка в sandbox

### Сборка через CI

Сборка запускается автоматически на коммиты в транк: https://a.yandex-team.ru/projects/ticket/ci/actions/launches?dir=travel%2Favia%2Fdevops%2Fdeploy_solomon_agent&id=build

### Локальная сборка

```
$ ya package --checkout --tar --upload --sandbox --owner=AVIA travel/avia/devops/deploy_solomon_agent/pkg.json
```

## Настройка stage в Deploy

Актуальную версию ресурса можно узнать в sandbox: https://sandbox.yandex-team.ru/resources?type=AVIA_DEPLOY_SOLOMON_AGENT_PACKAGE&attrs=%7B%22released%22%3A%22stable%22%7D

1. В настройках "Deploy unit" заходим во вкладку "Disk, volumes and resources"
2. Добавляем новый "Layer":
    - id: `solomon-agent`
    - URL: ссылка на sandbox-ресурс, например `sbr:3298714622`
3. Добавляем новый "Box". Отдельный box нужен для того, чтобы обновление solomon-agent не приводило к редеплою самого приложения.
    - id: `solomon-agent`
4. В настройках "Box" заходим во вкладку "Resources" добавляем слой с Ubuntu и слой `solomon-agent`
5. Добавляем новый "Workload":
    - id: `solomon-agent`
    - Init command: `/solomon/bin/pre_start --source=/solomon/agent.conf.template --destination=/solomon/agent.conf`
    - Start command: `/solomon/bin/solomon-agent --config=/solomon/agent.conf`
    - Readiness probe: TCP на порт `8383`
6. Настраиваем релизное правило (sandbox release rule) для автообновления:
    - Release types: соответственно стейджу, например для `unstable` выбираем `prestable, stable, testing, unstable`
    - Task type: `YA_PACKAGE_2`
    - Resource type: `AVIA_DEPLOY_SOLOMON_AGENT_PACKAGE`
    - Target: layer `solomon-agent`

### Важные замечания

1. Если используются `Mount volumes` нужно их примонтировать к box с solomon-agent, для мониторинга места на диске.
