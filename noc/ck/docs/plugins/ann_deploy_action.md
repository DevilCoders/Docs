# ann_deploy - сгенерировать и задеплоить конфиг Аннушкой

## Обзор {#synopsis}
Вызывает `ann deploy` для снуления diff конфигурации на сетевом устройстве.

Версия аннушки зафиксирована в сабмодуле [modules/annushka](https://noc-gitlab.yandex-team.ru/nocdev/noc-ck/-/tree/master/modules) и обновляется по запросу в nocdev.

## Параметры {#parameters}

Параметр | Комментарий
:--- | :---
`gens` - _list_ / **optional** | Список генераторов (тегов генераторов), которые необходимо вызвать, по умолчанию вызываются все генераторы.
`no_gens` - _list_ / **optional** | Список генраторов (тегов генераторов), которые не надо вызывать, по умолчанию списко пустой.
`filter_acl` - _text_ / **optional** | ACL фильтр для применения только того diff который попадает под указанный ACL, можно использовать селекторы по `hw`, что бы ACL можно было задавать повендорно.
`filter_peer` - _string_ / **optional** | Фильтрация diff по пиру в Racktables.
`retries` - _integer_ / **optional** | Количество попыток применения diff, каждая попытка запускается если применение diff было неудачным.
`hosts` - _list_ / **optional** | Список хостов на которых надо применять diff, по умолчанию применяется на хосте для которого запущен сценарий. Если в списке надо указать хост на котором запущен сценарий, то следует использовать зарезервированное имя хоста - `self`.

## Примеры {#examples}
Пример эквивалентный запуску `ann deploy -g rpl,l3 -G qos`

```yaml
- name: drain spine
  ann_deploy:
    gens:
      - rpl
      - l3
    no_gens:
      - qos
```

Запуск модуля с фильтрами ACL сразу на двух хостах

```yaml
- name: ann deploy test
  ann_deploy:
    gens:
      - iface
    retries: 3
    filter_acl:
    - hw: hw.Nexus
      text: |
        interface
         description
    hosts:
      - n9k-9316-test
      - n3k-3432-test
```
