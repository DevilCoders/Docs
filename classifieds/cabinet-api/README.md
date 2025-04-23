# Подготовка к работе

1. Воспользоваться [shiva-conf](https://a.yandex-team.ru/arcadia/classifieds/infra/shiva-conf) чтобы достать и разложить по конфигам значения, либо воспользоваться [готовыми conf-файлами](https://yav.yandex-team.ru/secret/sec-01g5h700kvyr64pr9wx9zcr98k/explore/versions)
2. При запуске локально надо не забыть заменить походы в базки через консул на реальные сервера. Их можно найти [тут](https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-mysql/cluster/mdbtsj5h5n2mn34nln1f?section=databases)
3. Подготовить директорию для дататайпов:

```
sudo mkdir -p /var/lib/yandex/autoru-cabinet/cabinet-api/autoru-extdata/
sudo chown -R $whoami /var/lib/yandex/autoru-cabinet/cabinet-api
```

### Дополнительные моменты на старте
— При запуске через sbt run иногда возникает проблема с резолвингом имен zookeeper - в таком случае может помочь запуск из IDEA(кнопка возле MainApp).

— Также не забыть, что кабинет выгружает каталог авто, выделить ему на это 4+ гб (подбиралось наугад, может меньше, может больше) оперативной памяти.

— Иногда при подгрузке дататайпов CarsOfferStat происходит ошибка с несуществующей секцией - в этом случае можно просто в месте парсинга данных возвращать всегда ```Section.Used```

— (mac) Если на машине запущен Docker, но testcontainers говорит, что не может найти подходящее окружение, в настройках докера снять пункт "gRPC FUSE"

— (mac) Docker Desktop на MacOS не рекомендуется использовать из-за лицензионных ограничений.
В качестве альтернативы можно использовать [colima] или [podman].

[colima]: https://docs.yandex-team.ru/classifieds-infra/verticals-backend/quick-start/docker
[podman]: https://wiki.yandex-team.ru/users/vladvershinin/notes/docker-i-testcontainers-cherez-podman-na-macos

— (mac m1) Если при скачивании образов вылезает ошибка про неподходящую архитектуру, то можно либо а) руками выкачать образ командой `docker pull` с указанием подходящей платформы через `--platform`, либо б) в MySqlContainer добавить
`c.addParameter("--platform", "linux/x86_64")`, либо в) в коде поменять контейнер mysql на внешний.

# Релиз в тестинг / продакшн
Осуществляется с использованием TeamCity и Shiva следующим образом:
1. Запустить соответствующую джобу в TC для релиза в тестинг:

   — [cabinet-api](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_AutoruCabinet_ArcadiaAutoruCabinetApiRelease)

   — [cabinet-scheduler](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_AutoruCabinet_AutoruCabinetSchedulerReleaseArcadia)

2. После релиза в тестинге и проверки, релиз на продакшн можно осуществить посредством кнопки `promote` в соответствующих
разделах админки:

    — [cabinet-api](https://admin.vertis.yandex-team.ru/services/autoru-cabinet-api)

    — [cabinet-scheduler](https://admin.vertis.yandex-team.ru/services/autoru-cabinet-scheduler)

Некоторые подробности можно также посмотреть [в документации](https://docs.yandex-team.ru/classifieds-infra/deploy/quick-start).

# Форматирование кода
В этом проекте используется [scalafmt](https://scalameta.org/scalafmt/) для форматирования кода.
Для того, чтобы отформатировать весь код необходимо запустить:
```
make fmt
```

Таким образом запускается форматирование всех файлов, изменённых относительно мастера.
На случай проблем, можно запустить форматирование абсолютно всех файлов (оно обычно сильно дольше):
```
make full-fmt
```

В новых версиях IDEA scalafmt подключается автоматически.
В более старых нужно устанавливать плагин.
1. Settings -> Plugins -> Browse repositories... -> найти scalafmt -> Install
2. Рестартовать IDEA
3. Ctrl/Command+Shift+L, чтобы отформатировать файл

# Фичи

Логику, которую хочется менять в рантайме без деплоя, можно заворачивать в фичу.

Пример получения списка фичей с их значениями:
`curl 'http://$hostname:2030/api/1.x/features'`

Пример обновления значения фичи:
`curl -X PUT 'http://$hostname:2030/api/1.x/features/call-placement' -d 'true''`
где call-placement -- имя фичи, true -- новое значение фичи (передаётся в теле запроса).

После такого обновления в коде, в котором используется эта фича, её значение станет `true`.

Фичи хранятся в ZooKeeper.
При инициализации сервисов, если не удалось создать клиент ZooKeeper для работы с фичами,
зажигается мониторинг. Также производится фоллбек, чтобы не ронять весь сервис:
все значения фич становятся дефолтными.

# Дашборды

- [Нагрузка на s3](https://grafana.vertis.yandex-team.ru/d/ihuKVu5Gz/cabinet-api-and-tasks)
- [Нагрузка на API кабинета](https://grafana.vertis.yandex-team.ru/d/RQ-pvcfik/cabinet-api-requests)
