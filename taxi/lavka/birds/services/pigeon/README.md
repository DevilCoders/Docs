# lavka-pigeon

---

## Quick Start

Для dev разработки:

1.  ```bash
    # Добавляем dev домен в /etc/hosts
    echo '127.0.0.1 pim.dev.lavka.yandex-team.ru' | sudo tee -a /etc/hosts
    ```

1.  ```bash
    # Запускаем каждый раз при значительных изменениях в коде или npm зависимостях
    # (должен быть добавлен ssh ключ из профиля на staff-е: ssh-add /path/to/rsa или ssh-add -K для mac os)
    npm run dev:install
    ```

1.  ```bash
    # Запускаем все сервисы и следим за изменениями в коде
    pigeon dev
    ```

### Tips and Tricks

*   Запуск вспомогательных сервисов и приложения отдельно:

    ```bash
    # В первом терминале запускаем сервисы
    pigeon start services
    # Во втором терминале приложение и watcher-ы
    pigeon dev -S
    # или так (простой запуск на localhost:3000)
    pigeon dev -S --authMocks --noHttps
    ```

*   Запуск с `React-Fast-Refresh`:

    ```bash
    pigeon dev --hot
    ```

*   Запуск с тестовыми (фейковыми) данными:

    ```bash
    pigeon dev --seedDb
    # или налить данные в уже запущенное приложение
    pigeon db fill
    ```

*   Не компилируйте тесты при запущенном `pigeon dev`! Можно сразу запускать тесты:

    ```bash
    pigeon test -C
    # или отдельный файл
    pigeon test -C -p <путь_к_файлу_теста>
    ```

### Troubleshooting

Если приложение перестало запускаться после `pull`-а, то возможно надо пере-накатить миграции на чистую БД.

Для этого останавливаем процесс `pigeon dev` и выполняем команды:

```bash
docker-compose down -v
npm run dev:install
pigeon dev
```

Если ничего не помогает:

```bash
docker-compose down -v
docker system prune -a -f
npm run dev:install
pigeon dev
```

Собрать и проверить локально прод сборку:

```bash
NODE_ENV=production pigeon compile
NODE_ENV=production WITH_AUTH_MOCKS=1 node out/server/index.js
```

---
## Documentation

*   [Contributing](CONTRIBUTING.md)
*   [Работа с БД](../../docs/db.md)
*   [Command Line Interface](docs/cli.md)
*   [Переводы](docs/tanker.md)
*   [Клиент-серверное взаимодействие](docs/client-server.md)
*   [RTC](docs/rtc.md)
*   [Тестирование](docs/test.md)
*   [Выкатка релизов](docs/release.md)
*   [Клиентские ошибки](docs/client-errors.md)
*   [Нагрузочное тестирование](docs/load-testing.md)
*   [Realtime конфиги](docs/real-time-configs.md)

---
## Клоундуктор

| Service | Link |
|---|---|
| Голубь | https://tariff-editor.taxi.yandex-team.ru/services/35/edit/355497/info |
| БД Голубя | https://tariff-editor.taxi.yandex-team.ru/services/35/edit/355498/info |
| Секреты | https://tariff-editor.taxi.yandex-team.ru/secrets?project_name=lavka&service_name=pigeon |

---
## Site hosts
| Environment | Link |
|---|---|
| dev | https://pim.dev.lavka.yandex-team.ru:3000 |
| unstable | https://pim.unstable.lavka.yandex-team.ru |
| unstable2 | https://pim.unstable2.lavka.yandex-team.ru |
| testing | https://pim.tst.lavka.yandex-team.ru |
| pre-stable | https://pim.pre.lavka.yandex-team.ru |
| stable | https://pim.lavka.yandex-team.ru |

---
## Логи

[Маппинг ключей Кибаны](https://nda.ya.ru/t/iCWq65eU4JNiWY)

| Environment | Link |
|---|---|
| testing | https://nda.ya.ru/t/4J3ZgnXa49HfzT |
| stable | https://nda.ya.ru/t/ngE78PcL49Hg39 |

### Логи в YT
| Name | Link |
|---|---|
| YT папка | https://nda.ya.ru/t/1wn-ADD_4NP4ER |
| LogBroker Topic | https://logbroker.yandex-team.ru/logbroker/accounts/taxi/lavka-pigeon-app-log |

### Nginx логи в YT
| Name | Link |
|---|---|
| YT папка | https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/taxi-access-log |
| Пример YQL | https://yql.yandex-team.ru/Operations/YVQ1ghJKffsvoqciW-sc5aEjbFObCiXs1bk-OmjZt7g= |

---
## Графики и алерты

| Environment | Link |
|---|---|
| testing | https://grafana.yandex-team.ru/d/t6HyW8wGz/nanny_lavka_pigeon_testing |
| stable | https://grafana.yandex-team.ru/d/wijpWUwMz/nanny_lavka_pigeon_stable |

### Графики базы данных
| Environment | Link |
|---|---|
| unstable | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb0c5mo21ed78ugvq5e;dbname=pigeon/ |
| testing | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbeoj63bndl0l3ep43h;dbname=pigeon/ |
| stable | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb2amg9tq2u94kcf9b4;dbname=pigeon/ |

### Конфиги графиков

| Environment | Link |
|---|---|
| testing | https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs/grafana/nanny_lavka_pigeon_testing.yaml |
| stable | https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs/grafana/nanny_lavka_pigeon_stable.yaml |

### Dorblu конфиги

| Environment | Link |
|---|---|
| testing | https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs/dorblu/lavka/nanny.lavka_pigeon_testing.yaml |
| stable | https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs/dorblu/lavka/nanny.lavka_pigeon_stable.yaml |

### Juggler конфиги

| Environment | Link |
|---|---|
| testing | https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-juggler/checks/taxi.lavka.test/rtc_lavka_pigeon_testing |
| stable | https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-juggler/checks/taxi.lavka.prod/rtc_lavka_pigeon_stable |

*   [Telegram "lavka-pigeon-alerts"](https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-juggler/telegram_options)
*   [error-booster juggler alerts](https://nda.ya.ru/t/-hYmw4XY4AVXTb)

---
## Метрики и сигналы

### Monitoring Dashboards

https://monitoring.yandex-team.ru/projects/lavka_pigeon/dashboards

---
## Secrets

### `pigeon.readonly`: database connection (READ-ONLY)
| Environment | Link |
|---|---|
| unstable | https://yav.yandex-team.ru/secret/sec-01fbpgym8y2qq85pfj4cwqth4t/explore/versions |
| testing | https://yav.yandex-team.ru/secret/sec-01f1prttbag90zkdsmd6zdfs8t/explore/versions |
| stable | https://yav.yandex-team.ru/secret/sec-01f1prh54vqfnmv0q09rxgf90r/explore/versions |

*   [pigeon.dev](https://yav.yandex-team.ru/secret/sec-01f1yk7z7g01hg61ax5p528xcq/explore/versions)
    <br/>используются при локальной разработке и автоматически подтягиваются при запуске `npm run dev:install`
*   [robot-pigeon](https://yav.yandex-team.ru/secret/sec-01f2h3qkgex6jmjf7sbr5tfzxy/explore/versions)
*   [robot-pigeon-credentials](https://yav.yandex-team.ru/secret/sec-01fdc44h6qtebp4h0a187gx472/explore/versions)
*   [robot-pigeon-ssh](https://yav.yandex-team.ru/secret/sec-01f2mfb3b4d58w7hrakpg6tbjy/explore/versions)
*   [pigeon.ci](https://yav.yandex-team.ru/secret/sec-01f2haqvtt2bdga001j4qpkqc4/explore/versions)
    <br/>секреты для TeamCity

---
## Выгрузка DMP

### Скоуп правил

| Environment | Link |
|---|---|
| testing | https://tariff-editor.taxi.tst.yandex-team.ru/replications/show/pigeon |
| stable | https://tariff-editor.taxi.yandex-team.ru/replications/show/pigeon |

### Таблиц

| Environment | Link |
|---|---|
| testing | https://yt.yandex-team.ru/hahn/navigation?path=//home/lavka/testing/replica/postgres/pigeon |
| stable | https://yt.yandex-team.ru/hahn/navigation?path=//home/lavka/production/replica/postgres/pigeon |

---
## Аватарница

### Неймспейс

Ссылка в неймспейсницу ([документация](https://wiki.yandex-team.ru/mds/avatars/nscfg/)): https://mds.yandex-team.ru/avatars/namespaces/lavka-pigeon/overview

### Графики

| Environment | Link |
|---|---|
| testing | https://yasm.yandex-team.ru/template/panel/avatars_mds/dashboard=short;ns=lavka-pigeon;ctype=testing |
| stable | https://yasm.yandex-team.ru/template/panel/avatars_mds/dashboard=short;ns=lavka-pigeon;ctype=production |
