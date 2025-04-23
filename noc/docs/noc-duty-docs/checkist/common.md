# Чекист

## Что это такое

Чекист - это система запуска генерации конфигов [аннушкой](../annushka/katka.md). Бизнесово он выполняет три задачи:
  - гоняет регрессионные тесты для MR в Аннушку. Генерятся конфиги для мастера и для новой ветки. Результат сравнивается и если есть дифф, он выводится пользователю для ознакомления. Интерфейс для пользователя - пайплайны в Гитлабе.
  - считает диффы для Дифалки. После каждого коммита в мастер аннушки для каждого устройства из [определённого списка](https://a.yandex-team.ru/arc/trunk/arcadia/admins/salt-media/noc/roots/units/nocdev-4k/files/etc/checkist/config.json?rev=r8822726#L5) запускается генерация конфигов, диффов и патчей. Результаты потом можно посмотреть в [сответствующем интерфейсе](https://noc.yandex-team.ru/diffs).
  - служит источником списка данных из RT (устройства и теги) для [noc.yandex-team.ru](https://noc.yandex-team.ru/devices). Какие именно девайсы там показываются, см. [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/admins/salt-media/noc/roots/units/nocdev-4k/files/etc/checkist/config.json?rev=r8822726#L4).

## Где что искать
- fqnd VS'a: [прод](https://chk.yandex-team.ru/), [тест](https://chk-test.yandex-team.ru/);
- рилы: [прод](https://racktables.yandex-team.ru/index.php?page=macros&macro_name=_C_NOCDEV_4K_), [тест](https://racktables.yandex-team.ru/index.php?page=macros&macro_name=_C_NOCDEV_TEST_4K_);
- графички: [дашборд](https://graf.yandex-team.ru/d/Cn_-Kli7z/checkist), [все метрики](https://solomon.yandex-team.ru/?project=noc&cluster=checkist&service=checkist), [статистика по диффам](https://datalens.yandex-team.ru/myq3sqesiexog-total-cfg-diff-counts);
- агрегаты: [в джагглере](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dnocdev-4k), [в мондате](https://noc-gitlab.yandex-team.ru/nocdev/mondata/-/blob/master/kulebyaks/nocdev-4k.yaml);
- [код](https://a.yandex-team.ru/arc/trunk/arcadia/noc/checkist), [конфиги](https://a.yandex-team.ru/arc/trunk/arcadia/admins/salt-media/noc/roots/units/nocdev-4k/);
- [пайплайн выкатки](https://tsum.yandex-team.ru/pipe/projects/nocdev/delivery-dashboard/checkist/);
- логи надо смотреть на рилах, удобнее через [executer](https://wiki.yandex-team.ru/executer/).

## Если зажёгся алерт
### cron_* и finalize_workers
Упала какая-то периодическая джоба. Надо пойти посмотреть логи systemd-сервиса `checkist-cron` на указанном хосте. Код самих джобов начинается [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/noc/checkist/checkist/cron.py).
### api_revs_create и api_test
Не удалось соответственно запустить генерацию новой ревизии диффов или регрессионные тесты. Надо смотреть логи systemd-сервиса `checkist-api` на указанном хосте в поисках ошибки.
### nocdev-4k-weblua-log-5xx
Больше 10 штук 500-к в логах nginx за последний час. Надо смотреть логи `checkist-api` или nginx.
### new_revisions
В мастере аннушки есть новый коммит, прошло более 2-х часов, но новая ревизия так и не сгенерировалась. Надо начать с вывода [джобы в Гитлабе](https://noc-gitlab.yandex-team.ru/nocdev/annushka/-/jobs) там, где stage - `after-merge`. Там либо будет видно ошибку, либо айдишник ревизии на стороне Чекиста. Его нужно поискать в логах и посмотреть, что произошло.
### last_rev_status
Последняя ревизия сгенерилась с ошибкой. Надо смотреть логи `checkist-cron` в поисках причин.

## Что ещё может случиться
### Сдают ошибку в CI-джобе регресионных тестов
Там обычно есть трейсбек. Кроме очевидного чтения логов проблемы могут быть на стороне стейджинга RT (видно по упоминанию RT в ошибке, надо сдать соответствующей команде) и на стороне генерации [cli для Чекиста в Сэндбоксе](https://sandbox.yandex-team.ru/resources?type=NOC_CHECKIST_BINARY_RESOURCE).

### Каких-то хостов нет в списке девайсов на [noc.yandex-team.ru](https://noc.yandex-team.ru/devices).
Править [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/admins/salt-media/noc/roots/units/nocdev-4k/files/etc/checkist/config.json?rev=r8822726#L4).

### Для каких хостов не посчитались диффы
Посмотреть, попадает ли хост в [рэккод](https://a.yandex-team.ru/arc/trunk/arcadia/admins/salt-media/noc/roots/units/nocdev-4k/files/etc/checkist/config.json?rev=r8822726#L5). Посмотреть ошибки генерации (на [noc.yandex-team.ru/diffs](https://noc.yandex-team.ru/diffs) рядом со словами "Current revision" есть процентики, если на них навести, можно увидеть список трейсов). Если не помогло, читать логи генерации в `checkist-cron`. Надо учитывать, что существующий конфиг берётся не наживую с устройства, а из репозитория [gfglister](https://docs.yandex-team.ru/gfglister).
