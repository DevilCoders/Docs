# Заведение juggler-проверок через directadmin-make-juggler.py

## Теория

У нас есть скрипт [directadmin-make-juggler.py](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/directadmin-juggler/bin/directadmin-make-juggler.py).
Он умеет чекаутить из репозитория скрипты и запускать их с параметрами про juggler.

Используем так: 

- регулярно запускаем с ppcback-ов, [кронтаб](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/ppcback-directadmin-cron/etc/cron.d/yandex-du-ppcback-directadmin-cron#L33)
- в каталоге [checks](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/directadmin-juggler/checks) пишем скрипты, которые заводят проверки

Обычно скрипт в каталоге `checks` заводит проверки по каким-то конфигам/реестрам:
реестр приложений, реестр подсистем и т.п.

### Контракт для "модулей" (скриптов в checks) { #modules }

Если пользоваться `add_default_args` аналогично существующим скриптам, то параметры получатся автоматически.

Если хочется все вручную, то скрипт из каталога `checks` должен поддерживаать параметры:

- `--apply` &mdash; применить изменения
- `-v` &mdash; вывести подробный дифф
- `-t` &mdash; где брать токен вместо `~/.juggler-token`
- `-p` &mdash; красивый вывод (pretty)



## Позапускать заведение проверок, поотлаживать { #debug }

Делаем на ppcdev там уже есть/должны быть нужные библиотеки - juggler-sdk (ppcdev не любой, точно было на ppcdev7).

### (Однократно) получить токен для juggler { #auth }

Взять токен по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=cd178dcdc31a4ed79f42467f2d89b0d0), положить его в файл `~/.juggler-token`

### Посмотреть, какие изменения будут делаться в проверках { #run-script }

Запускать скрипты из каталога `checks` с параметром `-v`.
Они будут писать дифф в проверках, применять в juggler ничего не будут. 

Пример: 

```text
$ ./checks/direct.np_javaperl.py -v
[2020-08-26 14:23:01,764]       check updated: (direct.np) direct.np_javaperl:access_check.db-test, diff: {"changes": {"tags": {"current": ["direct-access-check-np", "a_mark_direct.np_javaperl"], "desired": ["direct-access-check-np-2", "a_mark_direct.np_javaperl"]}}}
[2020-08-26 14:23:01,764]       check updated: (direct.np) direct.np_javaperl:access_check.db-devtest, diff: {"changes": {"tags": {"current": ["direct-access-check-np", "a_mark_direct.np_javaperl"], "desired": ["direct-access-check-np-2", "a_mark_direct.np_javaperl"]}}}
[2020-08-26 14:23:01,764]       check updated: (direct.np) direct.np_javaperl:access_check.db-dev7, diff: {"changes": {"tags": {"current": ["direct-access-check-np", "a_mark_direct.np_javaperl"], "desired": ["direct-access-check-np-2", "a_mark_direct.np_javaperl"]}}}
[2020-08-26 14:23:01,765]       check updated: (direct.np) direct.np_javaperl:access_check.metrika-audience-intapid-test, diff: {"changes": {"tags": {"current": ["direct-access-check-np", "a_mark_direct.np_javaperl"], "desired": ["direct-access-check-np-2", "a_mark_direct.np_javaperl"]}}}
[2020-08-26 14:23:01,824]       dry_run: True, changed:   4 (inserted:   0, updated:   4, removed:   0), total: 4
```

## Применить новые настройки { #apply }

**В норме вручную запускать применение настроек не надо.** Это неполезно и даже вредно.
Настройки будут перезатираться регулярными запусками с ppcback,
а после каждого обновления параметров проверка на 20 минут попадает в даунтайм. 

Если новые настройки хороши &mdash; надо закоммитить скрипт и дождаться регулярного применения. 

Если все-таки надо вручную применить: запустить скрипт из каталога `checks` с параметром `--apply`:

```text
./checks/direct.np_javaperl.py -v --apply
```

## Сделать новые проверки { #new-checks }

Написать новый скрипт в каталоге `checks` по аналогии с каким-нибудь старым или модифицировать подходящий существующий скрипт, отладить по [рецепту выше](#debug), закоммитить.

Не жесткое требование, но соглашение: неймспейс и хост проверки извлекать из имени файла, см. вызов `get_namespace_host` в существующих модулях.

## Ссылки { #links }

- [Документация по Juggler](https://docs.yandex-team.ru/juggler)
- [Про аутентификацию в Juggler](https://docs.yandex-team.ru/juggler/authentication#namespace-access)
- [Историческое описание заведения проверок в Директе](https://wiki.yandex-team.ru/jeri/monitoring-alerting/#adminskiemonitoringi)
- [Тестирование звонящих мониторингов на примере ppcdata](https://wiki.yandex-team.ru/jeri/monitoring-alerting/#direkt-testirovaniezvonjashhixmonitoringovmysqlnaprimereppcdata)
