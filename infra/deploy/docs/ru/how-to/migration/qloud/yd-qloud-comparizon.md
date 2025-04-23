# Таблица соответствия сущностей Y.Deploy и QLoud

Страница содержит перечень сущностей и настроек Qloud и Y.Deploy, соответствие которых вызывает вопросы у пользователей.

Соответствия может не быть по нескольким причинам:

- Функциональность ещё не поддержана в Y.Deploy.
- Функциональность поддержана не в Y.Deploy, а в awacs или Yav.
- Y.Deploy и Qloud — разные сервисы, отличающиеся друг от друга по архитектуре, реализации и возможностям.

## Есть и в Qloud и в Y.Deploy {#all}

| **QLoud** | **Y.Deploy** | **Доп. информация** |
|---|---|---|
| Проект | [Проект](../../../concepts/project.md) | В обеих системах проект — это сущность верхнего уровня, к которой привязывается расход квоты. Функционально они не полностью идентичны.|
| Окружение | [Stage](../../../concepts/stage/stage.md) + awacs + yav | Инстансы запускаются в Y.Deploy, балансировка настраивается в [awacs](https://wiki.yandex-team.ru/cplb/awacs), секреты хранятся в [yav](https://wiki.yandex-team.ru/passport/yav-usage). |
| Компонент | [Deploy Unit](../../../concepts/deploy-unit/deploy-unit.md) | |
| JugglerClient | Sidecar [Juggler subagent](../../../concepts/pod/sidecars/jugglersubagent.md) | |
| tvmConfig | Sidecar [TVM tool](../../../concepts/pod/sidecars/tvmtool.md) | `$QLOUD_TVM_TOKEN -> $TVMTOOL_LOCAL_AUTHTOKEN` |
| [DeployPolicy.Inplace](https://wiki.yandex-team.ru/qloud/doc/environment/component/#inplace) | Multi Cluster | Схема управления кластером соответствует [примитиву деплоя](../../../concepts/deploy-unit/deploy-primitives.md) Multi Cluster в Y.Deploy. |
| I/O | Disk Bandwidth | Прямого соответствия между параметрами нет.<br/>В QLoud `I/O` устанавливается в процентах и отвечает за количество инстансов, которое можно запустить на одном физическом хосте. Сумма `I/O` для всех инстансов на хосте не должна превышать 100.<br/>В Y.Deploy параметры `Disk Bandwidth` устанавливают гарантированную и максимально возможную скорость чтения/записи диска в байтах в секунду.  |
| Project Network | Network Macros | |
| Status Hooks | Readiness probe | В Y.Deploy также есть `Liveness probe`, которому нет аналога в Qloud.|
| Features | Ограниченная поддержка | `CAP_NET_ADMIN`, `CAP_NET_RAW`, `PORTO_SOCKET` поддержаны по умолчанию.<br/>`OS_CONTAINER` можно включить, выставив `workload.command=/sbin/init` в `deploy.yaml`.<br/>`ISS_RESOURCE_BIND_MOUNT` не используется, поскольку в Y.Deploy нет проблемы, ради которой создавалась эта фича в Qloud.<br/>`UNBOUND_CPU` не поддерживается. В Y.Deploy лимиты на CPU обязательны.<br/><br/>Всё, что не перечислено здесь, не поддерживается.|
| `routeSettings`, `domains`, `Heath check` и пр. параметры балансировки | [awacs](https://wiki.yandex-team.ru/cplb/awacs) | Всё, что относится к балансировке, реализовано через awacs.<br/><br/>Чтобы поддержать те же домены, что в и Qloud, необходимо для этих доменов выпустить сертификаты в awacs.|
| Настройки секретов | [Yav](https://wiki.yandex-team.ru/passport/yav-usage) | Y.Deploy работает с секретами через Yav. |
| Мониторинги | ([Мониторинги](../../../launch/monitorings.md)) | |
| Эфемерный диск | [Volume](../../../concepts/pod/volume.md) | |

## Есть в Y.Deploy, нет в Qloud {#deploy}

- Per-Cluster RS. Смотрите [Примитивы деплоя](../../../concepts/deploy-unit/deploy-primitives.md).
- Endpoint set. Смотрите [Deploy Unit](../../../concepts/deploy-unit/deploy-unit.md).
- Liveness probe

## Есть в Qloud, нет в Y.Deploy {#qloud}

- Приложение
- [BlueGreen](https://wiki.yandex-team.ru/qloud/doc/environment/component/#bluegreen)
- prepareRecipe

