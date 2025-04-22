# lavka-falcon

---

## Quick Start

Для dev разработки:

0.  ```bash
    # Добавляем dev-домен в /etc/hosts, чтобы работала авторизация:
    echo '127.0.0.1 falcon.dev.lavka.yandex-team.ru' | sudo tee -a /etc/hosts
    ```

1.  Для сборки opencv необходимо поставить `cmake`:
    ```bash
    sudo apt-get -y install cmake
    ```

    Или для mac:

    ```bash
    brew install cmake
    ```

    Далее необходимо поставить зависимости:

    ```bash
    # Запускается один раз для установки зависимостей и создания команды "falcon"
    # (должен быть добавлен ssh ключ из профиля на staff-е: ssh-add /path/to/rsa)
    npm run dev:install
    ```

2.  ```bash
    # Запускаем все сервисы и следим за изменениями в коде
    falcon dev
    ```

    *   ```bash
        # Альтернативно, можно запустить отдельно вспомогательные сервисы и приложение...
        # В первом терминале запускаем сервисы
        falcon start services
        # Во втором терминале приложение и watcher-ы
        falcon dev -S
        ```

### Troubleshooting

Если что-то пошло не так:
```bash
docker-compose down -v
docker system prune -a -f
npm run dev:install
falcon dev
```

---
## Documentation

*   [Contributing](CONTRIBUTING.md)
*   [Command Line Interface](docs/cli.md)
*   [Работа с БД](docs/db.md)
*   [Переводы](docs/tanker.md)
*   [Клиент-серверное взаимодействие](docs/client-server.md)
*   [RTC](docs/rtc.md)

---

## Клоундуктор

| Service | Link |
|---|---|
| Сокол | https://tariff-editor.taxi.yandex-team.ru/services/35/edit/355693/branches?service_name=falcon |
| БД Сокол | https://tariff-editor.taxi.yandex-team.ru/services/35/edit/355697/branches?service_name=falcon |
| Секреты | https://tariff-editor.taxi.yandex-team.ru/secrets?project_name=lavka&service_name=lavka-falcon |

---

## Site hosts
| Environment | Link |
|---|---|
| testing | https://falcon.tst.lavka.yandex-team.ru/ |
| pre-stable | https://falcon.pre.lavka.yandex-team.ru/ |
| stable | https://falcon.lavka.yandex-team.ru/ |

---
## Логи

| Environment | Project | Link |
|---|---|---|
| testing | falcon | https://nda.ya.ru/t/iwD4Na0j5Gg4Ct |
| testing | falcon-recognition | https://nda.ya.ru/t/meuverSF5Gg4BQ |
| stable | falcon | https://nda.ya.ru/t/jQCX9g695Gg3nu |
| stable | falcon-recognition | https://nda.ya.ru/t/EcI2Og6d5Gg3H9 |

### Nginx логи в YT
| Name | Link |
|---|---|
| YT папка | https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/taxi-access-log |
| Пример YQL | https://yql.yandex-team.ru/Operations/YuJ-o5fFt_3RbDfYIUKw82nm1cbJVTdNHSpeRfyByEg= |

---
## Графики и алерты

| Environment | Project | Link |
|---|---|---|
| testing | falcon | https://grafana.yandex-team.ru/d/xR3bgAg7k/nanny_lavka_lavka-falcon_testing |
| testing | falcon-recognition | https://grafana.yandex-team.ru/d/s5dxEVBnz/nanny_lavka_falcon-recognition_testing |
| stable | falcon | https://grafana.yandex-team.ru/d/JMGQqoRnk/nanny_lavka_lavka-falcon_stable |
| stable | falcon-recognition | https://grafana.yandex-team.ru/d/7VDmWSB7z/nanny_lavka_falcon-recognition_stable |

### Графики базы данных
| Environment | Link |
|---|---|
| testing | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbk916qsnrvtqhmiq9c;dbname=testing_lavka_falcon/ |
| stable | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbkddb2gpufr9lrl252;dbname=stable_lavka_falcon/ |

### Графики SQS
| Environment | Link |
|---|---|
| testing | https://monitoring.yandex-team.ru/projects/kikimr/dashboards/monk292eesvoinvqfugq?p.cluster=sqs&p.service=kikimr_sqs&p.host=cluster&p.user=lavka-falcon&p.queue=falcon-recognition-testing.fifo&from=now-1w&to=now&refresh=60000 |
| stable | https://solomon.yandex-team.ru/?project=kikimr&cluster=sqs&service=kikimr_sqs&host=cluster&dashboard=SQS&l.user=lavka-falcon&l.queue=falcon-recognition-production.fifo&b=1w&e= |

### Конфиги графиков

| Environment | Project | Link |
|---|---|---|
| testing | falcon | https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs/grafana/nanny_lavka_lavka-falcon_testing.yaml |
| testing | falcon-recognition | https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs/grafana/nanny_lavka_falcon-recognition_testing.yaml |
| stable | falcon | https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs/grafana/nanny_lavka_lavka-falcon_stable.yaml |
| stable | falcon-recognition | https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs/grafana/nanny_lavka_falcon-recognition_stable.yaml |

### Dorblu конфиги

| Environment | Project | Link |
|---|---|---|
| testing | falcon | https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs/dorblu/lavka/nanny.lavka_lavka-falcon_testing.yaml |
| testing | falcon-recognition | https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs/dorblu/lavka/nanny.lavka_falcon-recognition_testing.yaml |
| stable | falcon | https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs/dorblu/lavka/nanny.lavka_lavka-falcon_stable.yaml |
| stable | falcon-recognition | https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs/dorblu/lavka/nanny.lavka_falcon-recognition_stable.yaml |

### Juggler конфиги

| Environment | Project | Link |
|---|---|---|
| testing | falcon | https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-juggler/checks/taxi.lavka.test/rtc_lavka_lavka-falcon_testing |
| stable | falcon | https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-juggler/checks/taxi.lavka.prod/rtc_lavka_lavka-falcon_stable |

*   [Telegram "lavka-falcon-alerts"](https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-juggler/telegram_options)

---
## Secrets

### `falcon.readonly`: database connection (READ-ONLY)
| Environment | Link |
|---|---|
| testing | TODO |
| stable | https://yav.yandex-team.ru/secret/sec-01f8zpm369m1hrw4a7xpp5etpw/explore/versions |

*   [falcom.dev](https://yav.yandex-team.ru/secret/sec-01f85ax0m0jxj8dart1ktgdrzx/explore/versions)
    <br/>используются при локальной разработке и автоматически подтягиваются при запуске `npm run dev:install`
*   [robot-falcon](https://yav.yandex-team.ru/secret/sec-01f8zr6wgagjvbqgq8j424gnmg/explore/versions)
*   [robot-falcon-st-token](https://yav.yandex-team.ru/secret/sec-01fa4a01s613zt0t8cvszrq87b/explore/versions)
*   [falcon-jwt-secret](https://yav.yandex-team.ru/secret/sec-01fpebw8eymsw7zabmrrzdjbc3/explore/versions)
*   [falcon.1c](https://yav.yandex-team.ru/secret/sec-01fbm4gk1dc50vxe5p9j7m9q9e/explore/versions)
*   [falcon.ci](https://yav.yandex-team.ru/secret/sec-01f91k58124k69qc66zca7w4fw/explore/versions)
    <br/>секреты для TeamCity
