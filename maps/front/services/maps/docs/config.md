# Конфигурация

С конфигурацией в Картах все непросто. Этот документ поможет вам составить общую картину того, как настроить Карты и как добавить новые настройки.

## Основная конфигурация

Основная конфигурация Карт располагается в ряде файлов в директории `src/server/configs`; каждый конфиг соответствует одноименному окружению:

```
src/server/configs
    /development
    /testing
    /production
    /stand
    /stress
```

Для каждого из окружения есть три вида конфигурации:

-   `common.ts` — общая часть конфига для всех платформ и языков.
-   `platforms.ts` — конфиги, привязанные к типу платформы (`desktop`, `mobile`).
-   `localizations.ts` — конфиги, привязанные к языку.

1. Между собой они не пересекаются, т.е. друг друга они не расширяют и не наследуют.
2. Наследование между окружениями действует только в рамках отдельных конфигов.

Эти конфигурации содержат:

-   UI-настройки, влияющие на отображение тех или иных пользовательских элементов.
-   Технические настройки (например, сокет или тип сборки).
-   URL'ы к внешним сервисам.
-   Специфичные для проекта хосты.

В общем случае на сервере конфиг доступен в поле `req.config`. Если у вас нет доступа к `express.Request`, то используйте модуль конфига напрямую `server/config/config`.

## Хосты

Кроме собственной конфигурации, Карты также используют и общую для отдела Карт конфигурацию хостов. Эта конфигурация поставляется в виде Sandbox ресурсов:

-   hosts: https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=MAPS_CONFIG_HOSTS
-   inthosts: https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=MAPS_CONFIG_INTHOSTS

Многие хосты берутся из этих конфигов. В `inthosts` хосты, которые мы дергаем только с сервера, а в `hosts` те, что попадают на клиент и используются оттуда напрямую.

При локальной разработке хосты копируются с одного из разработческих серверов при помощи команды `make local-setup`.

Актуальные списки хостов можно найти в их репозитории:

|          |                                             testing (development)                                             |                                                 production (stand)                                                  |
| -------- | :-----------------------------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------: |
| hosts    |  [hosts-testing.json](https://a.yandex-team.ru/arc_vcs/maps/front/tools/hosts/hosts/1.3/hosts-testing.json)   |  [hosts-production.json](https://a.yandex-team.ru/arc_vcs/maps/front/tools/hosts/hosts/1.3/hosts-production.json)   |
| inthosts | [hosts-testing.json](https://a.yandex-team.ru/arc_vcs/maps/front/tools/hosts/inthosts/1.1/hosts-testing.json) | [hosts-production.json](https://a.yandex-team.ru/arc_vcs/maps/front/tools/hosts/inthosts/1.1/hosts-production.json) |

Для обновления пакетов хостов требуется найти в sandbox id соответствующего ресурса ([hosts](https://sandbox.yandex-team.ru/resources?type=MAPS_CONFIG_HOSTS) / [inthosts](https://sandbox.yandex-team.ru/resources?type=MAPS_CONFIG_INTHOSTS)) и указать новое значение в `tools/deploy/utils.js`.

### Переопределение хостов

#### [Переопределение через параметр host_config](https://a.yandex-team.ru/arc_vcs/maps/front/tools/hosts/README.md#pereopredeleniya-konfigov)

В `development` окружении хосты в конфигурации могут быть переопределены прямо в браузере. Для этого нужно добавить в запрос параметр `host_config[%host_type%][%host_id%]=%host_url%`.
Например, для того чтобы получать данные с production-версии поиска на локальном стенде, нужно открыть его по ссылке `https://%login%.maps.dev.yandex.ru:8080/maps/?host_config[inthosts][search]=http://addrs.yandex.ru:17140/`

### Принцип загрузки конфигов

Загрузка конфига зависит от режима работы сервера, который определяется с помощью модуля `src/server/lib/environment.ts`.

1.  Режимы `development`, `testing` и `production` интерпретируем буквально, `stand` как `production`, все остальные - как `testing`.
2.  Используем для загрузки конфига пакет `@yandex-int/maps-host-configs`, передав ему режим и перегрузки из запроса.
