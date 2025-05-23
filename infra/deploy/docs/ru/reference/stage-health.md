# Здоровье стейджа

Перечень возможных проблем конфигурации сервиса, которые в некоторых случаях могут приводить к его неработоспособности, и пути их устранения.

## Устаревшие ресурсы {#old-resources}

### Версия рантайма устарела {#code_old_runtime}
Предпочтительнее использовать последнюю версию рантайма, там много полезных [улучшений и исправлений](./patchers-revision.md#runtime-version-reviziya-shemy-patcherov.ms)
Следует помнить, что обновление версии рантайма всегда приводит к рестарту вокрлоадов и часто может вызывать реаллокацию подов.

### Версия инфра компонента устарела  {#code_old_sidecar}
Версия инфраструктурного сайдкара ([PodAgent](./pod-agent-releases.md)/[UnifiedAgent](https://docs.yandex-team.ru/unified_agent/release_notes) /TVMTools/DRU) ниже минимальной рекомендуемой, это может вызывать проблемы с работоспособностью сайдкаров для некоторых сервисов, в стабильных версиях устранены известные баги, рекомендуется регулярно обновлять сайдкары.
Следует помнить, что обновление подового зачастую приводит к рестарту всего пода, обновления же других сайдкаров будет вызывать рестарт только их.


## Мониторинг и алертинг {#monitoring}

### Не включены алерты сервис-провайдеров {#code_no_alerts}
[Алерты сервис-провайдеров](./alerts.md) позволяют узнать о проблемах с нехваткой ресурсов или падениях сервиса.

### Не собираются пользовательские метрики, используется коммунальный itype ("deploy") {#code_common_itype}
Если не указать itype для сбора метрик в сервисе, будет использоваться общий для всех `itype=deploy`, в котором в настоящий момент оверкоммит по квоте, это с высокой вероятностью приведёт к потери части как продуктовых, так и инфраструктурных метрик. Рекомендуется использовать [itype](../launch/monitorings.md#obshaya-informaciya) с квотой из собственного abc-сервиса.


## Проблемы с безопасностью {#security}

### Используется старая схема хранения секретов {#code_old_secrets}
От старой схемы хранения секретов планируется отказаться в ближайшем будущем, нужно выполнить миграцию, как это сделать и почему это важно можно прочитать [тут](../how-to/secrets.md#migraciya-so-staroj-na-novuyu-shemu.md).

### Сетевой макрос считается небезопасным {#code_dangerous_network}
Некоторые сетевые макросы не рекомендуются к использованию в production сервисах, например к `_SEARCHSAND_` есть доступ у всего поискового портала.


## Общие настройки сервиса {#common}

### Отсутствующие readiness пробы {#code_no_redness_probe}
У вокрлоада должны быть корректно настроены [пробы](../concepts/pod/workload/probes.md#liveness-readiness), это предотвратит выкатку сломанного релиза и защитит от других [проблем](https://clubs.at.yandex-team.ru/infra-cloud/2255)

### Нет лимитов анонимной памяти, лимитов на ворклоады в боксах с более чем одним ворклоадом {#code_no_anon_limit}
Подробнее о том, почему [лимиты анонимной памяти](../concepts/pod/pod.md#anonymous-memory-limit) важны. В новых [версиях рантайма](./patchers-revision.md) решены проблемы с зазором под кеш для сайдкаров, но если в одном боксе есть несколько пользовательских ворклоадов, рекомендуется установить для каждого из них лимиты.

### Кластер без подов, либо бюджет на недоступность может привести к даунтайму сервиса полностью или в локации{#code_dangerous_budget}
Настройки [disruption budget](../concepts/deploy-unit/deploy-primitives.md#disruption-budget) для локации может привести к недоступности локации при перевыкладке, аналогично для mcrs. Для некоторых сервисов это может быть важно, рекомендуется снизить бюджет.

### Rbtorrent без метаинформации используется в качестве ресурса  {#code_resource_protocol_problem}
Rbtorrent не является предпочтительным способом указания URL для ресурса, [подробности](../concepts/pod/podagentpayload/resources/resource-url.md). Всегда лучше указывать ссылку на sandbox-ресурс через `sbr:<resource_id>`. В этом случае доставляться в поды ресурсы будут также торрентами.

### Sandbox ресурс не имеет autobackup=true и имеет конечный ttl {#code_unknown_resource}
Для ресурса не настроен бэкап, это может привести к невозможности выкладки/переселения пода в случае поломки/недоступности единственного хоста, где этот ресурс хранился.


## Другое {#other}

### Владелец стейджа больше не сотрудник  {#code_no_owner}
Владелец стейджа — бывший сотрудник, в случае необходимости экстренно перевыкатить стейдж могут возникнуть проблемы с доступами, рекомендуется указывать abc-сервис в качестве владельца.

### Стейдж деплоился очень давно {#code_no_deploys}
Некоторые деплой-юниты успешно выкладывались более квартала тому назад, рекомендуется:
1. проверить, нужен ли вообще этот стейдж;
2. обновить сайдкары и версию рантайма;
3. устранить возможные обнаруженные за это время уязвимости.

### Стейдж долго не переходит в целевую ревизию {#code_not_deployed}
Деплой-юнит более суток не переходит в статус `ready`, подробности о причинах можно узнать на странице статуса стейджа. Также рекомендуется устранить все CRIT/WARN-предупреждения со страницы здоровья стейджа и если это не помогло, то заводить тикет в очередь [RTCSUPPORT](https://st.yandex-team.ru/createTicket?queue=RTCSUPPORT).

### Включен шедулинг через хинты {#code_scheduling_hints}
Для сервиса есть возможность настроить [scheduling_hints](https://a.yandex-team.ru/arcadia/yp/yp_proto/yp/client/api/proto/data_model.proto?rev=r9700013#L1379), что может привести к долгому деплою, попыткам деплоя в сегмент без квоты, вызвать другие неочевидные ошибки. Такая возможность нужна только нескольким сервисам, сообщение скорее информационное.
