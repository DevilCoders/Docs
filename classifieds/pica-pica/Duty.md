Pica-Pica duty
=================

- [Дока](https://wiki.yandex-team.ru/vertis/pica-pica/), вероятно, устаревшая.
- [Очередь VSCOMMONBACK](https://st.yandex-team.ru/VSCOMMONBACK)

## Конфигурация
Конфигурация сервиса `pica-pica-api` в `application.conf`, `core.conf` и файловых датасорсах.
Переменные окружения и секретница не используются.

## CI/CD
[Проект в тимсити](https://t.vertis.yandex-team.ru/project/VertisPicaPica?projectTab=overview&mode=builds)

В пуллреквестах аркадии автоматически запускается [CI Build (тесты)](https://t.vertis.yandex-team.ru/buildConfiguration/VertisPicaPica_ArcadiaCiBuild?mode=builds)

Сборка осуществляется через админский скрипт autorelease в [таске teamcity](https://t.vertis.yandex-team.ru/buildConfiguration/VertisPicaPica_ArcadiaPicaPicaApiRelease?mode=builds)

Таска запускается автоматически при изменении [changelog](./pica-pica-api/debian/changelog) в транке.

Можно запустить таску руками не из транка. В качестве версии в чейнджлоге можно указать снапшотную версию (например `0.2.23-feature-REALTYBACK-5990-sync-cache-clean-handle`).

Сперва собирается артефакт и выкладывается в [artifactory](https://artifactory.yandex.net/).
Затем скрипт создает тикет в кондукторе на деплой в кондукторе (сильно усторевший яндексовый CD):
- [Пакет](https://c.yandex-team.ru/packages/yandex-vertis-pica-pica-api)
- [Тикеты](https://c.yandex-team.ru/packages/yandex-vertis-pica-pica-api/tickets)
- [Пайплайн выкладки](https://c.yandex-team.ru/packages/yandex-vertis-pica-pica-api/deploy_list)
- [Хосты тестинга](https://c.yandex-team.ru/groups/vertis_vtest_realty_pica)
- Хосты прода (это железные коммуналки):
  - [sas](https://c.yandex-team.ru/groups/vertis_prod_shard)
  - [vla](https://c.yandex-team.ru/groups/vertis_vprod_shard)

После успешного деплоя в тестинг нужно нажать на тикете "в стейбл" - это запустит деплой на хосты прода.

Если нужно поставить более старую версию или зарестартить текущую,
нужно создать тикет руками и поставить галочку "Поставить более раннюю версию".

## Логи

### Логи пики
Логи пики файловые, льются и ротируются на `l.vertis.yandex.net`.
Логи лежат в коммунальных папках по хостам вида `/var/remote-log/$host/pica-pica/...`.
Хосты нужно смотреть в кондукторных группах прода (описано выше).


Список логов:
- `pica-pica-api.log` - основной лог приложения
- `pica-pica-api.log.shell` - лог запуска jvm
- `pica-pica-api-gc.log` - лог gc статистика
- `pica-pica-api-access.log` - access лог api пики
- `pica-pica-api-avatarnica.log` - синхронный лог запросов в аватарницу (body не логируется)
- `pica-pica-api-avatarnica-body.log` - асинхронный лог запросов в аватарницу (body логируется)


Логи предыдущих дней архивированны, так что их грепать через `zgrep` (будет дольше).

Пример запросов:

```bash
ssh l.vertis.yandex.net
```

```bash
grep img.carpp.ru /var/remote-log/shard-*.prod.vertis.yandex.net/pica-pica/pica-pica-api-avatarnica.log | grep -v 434
./shard-03-sas.prod.vertis.yandex.net/pica-pica/pica-pica-api-avatarnica.log:[2021-12-09 20:06:55,957] zDLP3XXskBQ GET http://avatars-int.mds.yandex.net:13000/put-autoparts-feed/vrkfjqg2apn1tj.1985122010?url=https://img.carpp.ru/a_images/300172/68_1228452946877233.jpg&expire=15552000s [] [] 15 502
grep img.carpp.ru /var/remote-log/shard-*.prod.vertis.yandex.net/pica-pica/pica-pica-api-avatarnica.log | grep 434 | wc -l
134370
grep img.carpp.ru /var/remote-log/shard-*.prod.vertis.yandex.net/pica-pica/pica-pica-api-avatarnica.log | grep -v 434 | wc -l
1
grep img.carpp.ru /var/remote-log/shard-*.prod.vertis.yandex.net/pica-pica/pica-pica-api-avatarnica.log | grep 434 | tail
./shard-03-vla.prod.vertis.yandex.net/pica-pica/pica-pica-api-avatarnica.log:[2021-12-09 20:02:05,004] HGbywXQF8q0 GET http://avatars-int.mds.yandex.net:13000/put-autoparts-feed/vrnqkg1q0gieej.947986818?url=https://img.carpp.ru/a_images/299977/56_1119778465668074.jpg&expire=15552000s [] [] 71 434
./shard-03-vla.prod.vertis.yandex.net/pica-pica/pica-pica-api-avatarnica.log:[2021-12-09 20:02:05,538] 5KWRlK7gDDY GET http://avatars-int.mds.yandex.net:13000/put-autoparts-feed/vrnqkgagnes2lv.646924452?url=https://img.carpp.ru/a_images/299977/64_855110106496104.jpg&expire=15552000s [] [] 94 434
```

### Логи аватарницы
- [Логи аватарницы в YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/avatars-mds-access-log)
- Пример запроса логов аватарницы по одному дню [(yql)](https://yql.yandex-team.ru/Operations/YbJoUpfFt-1ZIR6-GoEX-l_bXMhQZtuOuBQV0hikrLs=)
- Пример запроса логов аватарницы по нескольким дням дню [(yql)](https://yql.yandex-team.ru/Operations/YbJpYi3DcHav8dkCg_hoX79l5UsrTC2LWn_7riWiF9g=)

## Графики
Метрики пики устаревшие, не в прометеусе, а в графите (и его очень хотят закапывать админы).

### Графики пики
[Графики](https://grafana.vertis.yandex-team.ru/d/wiCSkN7ik/pica-pica) разбиты по доменам и группам хостов (смотрите про хосты в кондукторе).
Поэтому для прода нужно отдельно смотреть sas и vla.

### Графики аватарницы
[Графики в головане](https://yasm.yandex-team.ru/template/panel/avatars_mds/ns=realty/?range=2592000000) по неймспейсам (вероятно, лучше смотреть уже в новом monitoring ui).
Также у аватарницы есть [clickhouse view](https://avatars.chv.yandex-team.ru/projects/autoru-vos/projectDashboard?period=6hour) по неймспейсам.

### Графики кластеров кассандры
По интерпретации [графиков](https://grafana.vertis.yandex-team.ru/d/000000192/cassandra-clusters) можно спрашивать админов,
как и по всей эксплуатации кассандры.

Важное:
При запуске сервиса проверяется,
что кластеры кассандры по всем задекларированным (`ru.yandex.vertis.picapica.model.Service`) неймспейсам доступны.
Если какой-то из даже неиспользующихся кластеров удалят из кассандры,
сервис `pica-pica-api` не поднимется (в том числе будет невозможен откат или рестарт).
После одного такого инцидента админов предупредили, но гарантий нет.

## Support аватарницы
Из запина:
> ⚠️ В общем случае правильно сразу создавать задачу в очередь `MDSSUPPORT`, а сюда уже пинать 👞 ссылкой на тикет.

На самом деле, это не всегда так, иногда разумнее сперва спросить.

- [Ссылка на чат](https://t.me/joinchat/QNEQN5V5Id4A_gOC)
- [Очередь](https://st.yandex-team.ru/createTicket?queue=MDSSUPPORT)
- [Дока по чистому MDS](https://wiki.yandex-team.ru/mds/)
- [Дока по S3-api](https://wiki.yandex-team.ru/mds/s3-api/)
- [Дока по аватарнице](https://wiki.yandex-team.ru/mds/avatars/)
- [Логи MDS в YT](https://yt.yandex-team.ru/hahn/navigation?path=//logs/mds-access-log)
- [Логи S3 в YT](https://yt.yandex-team.ru/hahn/navigation?path=//logs/s3-access-log)
- [Логи аватарницы в YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/avatars-mds-access-log)


## Примеры тикетов, там полезное всякое:
- [Вопрос в mds по причинам непрокачки фоток через аву](https://st.yandex-team.ru/MDSSUPPORT-1907)
- [Тот же вопрос на стороне пики (там примеры получения логов)](https://st.yandex-team.ru/VSCOMMONBACK-58)
- [Комплексная проблема с кассандрой (конфиг + отключение одного из кластеров)](https://st.yandex-team.ru/VASUP-3469)
- [Тикет про закапывание Работы](https://st.yandex-team.ru/VSCOMMONBACK-64)

## FAQ
1. > Неймспейсы в аватарнице имеют какие-то различия? Кроме названий/лимитов на нагрузку и размеров самого неймспейса.
   > Слышал что там различия в мете - computer vision, но мб я что-то не понял

    Неймспейсы могут быть сильно различающимися. В частности, у них сильно отличается то, какую мету они требуют,
    какие там настройки ttl, на какие размеры нарезать, нужен ли оригинальный размер и т.д.
    В целом, это пользовательские неймспейсы, их настройки не на стороне пики.

4. > Не пробовали разделить лимит в аву для неймспейсов для получения и загрузки картинки?

    Нужно уточнять по доке авы, для каких групп запросов действуют какие ограничения. Не уверен, насколько это разумно.


3. > Так ли действительно необходим приоритет у загрузки картинок? Использовали ли вообще эту фичу?

    Вроде бы использовался для приоритетной прокачки изображений из ручных офферов.
    Нужно еще раз уточнить, насколько это нужно.

4. > Зачем нужна фича м перепрокачкой меты?

    При изменениях конфигурации метаинформации на неймспейсе авы, чтобы эти изменения были видны, мету нужно перепрокачать.

5. > Пика использует для идентификации картинки namespace + url. Почему не id переданный пользователем? Не говорили о таком?

    Говорили, поэтому в "новой" вообще решили не использовать внутренние id, а берем нормализованный url.

6. > Потребители не хотели получать инфу о готовности картинок/меты из топика кафки?

    Хотели, поэтому подумали про это в "новой".


### Еще что-то полезное можно найти в записи [техтока](https://wiki.yandex-team.ru/vertis/etc/tech-talks/)
(TODO - нужно выложить запись)
