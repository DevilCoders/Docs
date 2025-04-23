# lavka-eagle

---

## Quick Start

Для dev разработки:

1.  ```bash
    # Добавляем dev домен в /etc/hosts
    echo '127.0.0.1 eagle.lavka.dev.yandex-team.ru' | sudo tee -a /etc/hosts
    ```

1.  ```bash
    # Запускаем каждый раз при значительных изменениях в коде или npm зависимостях
    # (должен быть добавлен ssh ключ из профиля на staff-е: ssh-add /path/to/rsa или ssh-add -K для mac os)
    npm run dev:install
    ```

1.  ```bash
    # Запускаем все сервисы и следим за изменениями в коде
    eagle dev
    # или
    eagle fly
    ```

1.  ```bash
    # Запускаем все сервисы и запускаем импорт данных (Без данных сервис работать не будет)
    eagle dev --schedulers
    # или
    eagle fly --schedulers
    ```

1.  ```bash
    # Запускаем все сервисы и запускаем импорт данных только по москве (это минимальный набор)
    eagle dev --schedulers --importOnlyMoscow
    # или
    eagle fly --schedulers --importOnlyMoscow
    ```

### Tips and Tricks

*   Запуск вспомогательных сервисов и приложения отдельно:
    ```bash
    # В первом терминале запускаем сервисы
    eagle start services
    # Во втором терминале приложение и watcher-ы
    eagle dev -S
    # или так (простой запуск на localhost:3000)
    eagle dev -S --authMocks --noHttps
    ```

*   Запуск с `React-Fast-Refresh`:
    ```bash
    eagle dev --hot
    ```

*   Не компилируйте тесты при запущенном `eagle dev`! Можно сразу запускать тесты:
    ```bash
    eagle test -C
    # или отдельный файл
    eagle test -C -p <путь_к_файлу_теста>
    ```

*   Для отладки серверного кода в Visual Studio Code есть запуск сервера в debug режиме. Для этого необходимо поставить breakpoint,
    открыть Debugger (`⇧⌘D`), затем, если необходимо, выбирать конфигурацию для нужного вам сервиса (верхняя панель, `eagle`)
    и нажать "Start Debugging" (`F5`). При запросе к серверу должен подхватиться breakpoint в редакторе. Запрос не зарезолвится
    пока мы в редакторе не пройдём по всем breakpoint'ам.

### Troubleshooting

Если приложение перестало запускаться после `pull`-а, то возможно надо пере-накатить миграции на чистую БД.
Для этого останавливаем процесс `eagle dev` и выполняем команды:
```bash
docker-compose down -v
npm run dev:install
eagle dev
```

Если ничего не помогает:
```bash
docker-compose down -v
docker system prune -a -f
npm run dev:install
eagle dev
```

---
## Documentation

*   [Процесс разработки](docs/process.md)
*   [Contributing](CONTRIBUTING.md)
*   [Command Line Interface](docs/cli.md)
*   [Работа с БД](docs/db.md)
*   [Переводы](docs/tanker.md)
*   [Клиент-серверное взаимодействие](docs/client-server.md)
*   [RTC](docs/rtc.md)
*   [Тестирование](docs/test.md)
*   [Клиентские ошибки](docs/client-errors.md)
---
## Разработчику

### [Сервис в Клоундукторе](https://tariff-editor.taxi.yandex-team.ru/services/35/edit/355864/info)

*   [Сервис БД](https://tariff-editor.taxi.yandex-team.ru/services/35/edit/355878/info)

### Site hosts
| Environment | Link |
|---|---|
| dev | https://eagle.lavka.dev.yandex-team.ru:3000 |
| unstable | https://eagle.unstable.lavka.yandex-team.ru |
| unstable2 | https://eagle.unstable2.lavka.yandex-team.ru |
| testing | https://eagle.tst.lavka.yandex-team.ru |
| stable | https://eagle.prestable.lavka.yandex-team.ru |
| stable | https://eagle.lavka.yandex-team.ru |

### Логи в Кибане
*   **testing**
    *   [kibana](https://kibana.taxi.tst.yandex-team.ru/goto/75fd537bd4d29242c554955220e38a8c)

*   **prestable**
    *   [kibana](https://kibana.taxi.yandex-team.ru/goto/9c343036e903f5a5639f4fed423dd695)

*   **production**
    *   [kibana](https://kibana.taxi.yandex-team.ru/goto/cf7bb5055d6d39aaa4052200011299fd)

### Графики на сервис
*   **testing**
    https://grafana.yandex-team.ru/d/t6HyW8wGz/nanny_lavka_eagle_testing
    *   [grafana конфиг](https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs/grafana/nanny_lavka_eagle_testing.yaml)

*   **production**
    https://grafana.yandex-team.ru/d/wijpWUwMz/nanny_lavka_eagle_stable
    *   [grafana конфиг](https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs/grafana/nanny_lavka_eagle_stable.yaml)

### Сигналы
*   **testing**
    *   [dorblu конфиг](https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs/dorblu/lavka/nanny.lavka_eagle_testing.yaml)

*   **production**
    *   [dorblu конфиг](https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs/dorblu/lavka/nanny.lavka_eagle_stable.yaml)

### Алерты
*   **testing**
    *   [juggler конфиг](https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-juggler/checks/taxi.lavka.test/rtc_lavka_eagle_testing)

*   **production**
    *   [juggler конфиг](https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-juggler/checks/taxi.lavka.prod/rtc_lavka_eagle_stable)

---
## Secrets

### `eagle.readonly`: database connection (READ-ONLY)
| Environment | Link |
|---|---|
| testing | https://yav.yandex-team.ru/secret/sec-01f1prttbag90zkdsmd6zdfs8t/explore/versions |
| stable | https://yav.yandex-team.ru/secret/sec-01f1prh54vqfnmv0q09rxgf90r/explore/versions |

*   [eagle.dev](https://yav.yandex-team.ru/secret/sec-01f1yk7z7g01hg61ax5p528xcq/explore/versions)
    используются при локальной разработке и автоматически подтягиваются при запуске `npm run dev:install`
*   [robot-eagle](https://yav.yandex-team.ru/secret/sec-01f2h3qkgex6jmjf7sbr5tfzxy/explore/versions)
*   [robot-eagle-ssh](https://yav.yandex-team.ru/secret/sec-01f2mfb3b4d58w7hrakpg6tbjy/explore/versions)
*   [eagle.ci](https://yav.yandex-team.ru/secret/sec-01f2haqvtt2bdga001j4qpkqc4/explore/versions)
    секреты для TeamCity

---
## Dashboards

### Database
| Environment | Link |
|---|---|
| Unstable | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb2v67ggr5b1v8fhd39;dbname=eagle/ |
| Testing | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbgsc48qsb11rkccsfm;dbname=eagle/ |
| Stable | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbojg16r6qe8kmj8m8d;dbname=eagle/ |
