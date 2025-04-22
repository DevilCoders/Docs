# IMS

Сервис управления субъектами доступа

### Локальный запуск сервиса

#### С чего начать

 - Установите Arc и получите исходный код: https://docs.yandex-team.ru/devtools/intro/quick-start-guide
 - Установите Docker Compose: https://docs.docker.com/compose/install/
 - Авторизуйтесь в Docker: https://wiki.yandex-team.ru/docker-registry/#authorization
 - Запросите через IDM доступы на чтение к репозиториям ```registry.yandex.net/intranet/ims/imscore/imscore-backend``` и ```registry.yandex.net/intranet/ims/imscore/postgresql``` системы Docker-registry:
      - Доступ к образу с IMS: https://nda.ya.ru/t/9WDF0XxW57KtcS
      - Доступ к образу с PostgreSQL: https://nda.ya.ru/t/RumdO6wx57Ktsz

#### Запуск сервиса

1. Перейдите в директорию ```intranet/ims/imscore``` относительно корня Аркадии
2. Выполните команду

```
make start
```

Эта команда скачает образ сервиса и СУБД, после чего запустит сервис. Сервис будет доступен для запросов на ```localhost:8080```

#### Остановка сервиса

```
make stop
```

#### Удаление загруженных образов

```
make clean
```

#### Взаимодействие с сервисом

Для взаимодействия с сервисом нужна утилита grpcurl (https://github.com/fullstorydev/grpcurl), сам сервис доступен для запросов на ```localhost:8080```

Пример взаимодействия с сервисом:

```
grpcurl -plaintext -import-path ./backend/service/proto -proto healthz.proto localhost:8080 intranet.ims.imscore.backend.service.proto.Healthz/Readness
```

Ответ:

```
{

}
```

## Разработка

* [Source code](https://a.yandex-team.ru/projects/ims/code/intranet/ims/imscore)
* [Backend releases](https://a.yandex-team.ru/projects/ims/ci/releases/timeline?dir=intranet%2Fims%2Fimscore&id=backend-release)
* [Backend testing](https://deploy.yandex-team.ru/stages/imscore-test)


* Generate IDEA project: `ya ide idea ~/arcadia/intranet/ims/imscore --group-modules=tree --iml-in-project-root -r ~/IdeaProjects/imscore --with-content-root-modules --directory-based --generate-junit-run-configurations`


## Запуск тестов

Тесты расположены в директории:
```
~/arcadia/intranet/ims/imscore/backend/service/app/src/test/java/ru/yandex/intranet/imscore
```

Запуск всех тестов:
```
ya make -tt ~/arcadia/intranet/ims/imscore
```

После запуска тестов для всех упавших тестов будет выдана краткая информация о падениях (включая ссылки на более полную информацию). Для прошедших и проигнорированных (отфильтрованных) тестах будет выдан только общий короткий статус (количество тех и других).

Это поведение можно поменять следующими ключами:

    --fail-fast — исполнять тесты до первого падения.
    -P, --show-passed-tests — показывать каждый прошедший тест
    --show-skipped-tests — показывать каждый пропущенный (отфильтрованный) тест
    --show-metrics — показывать метрики тестов

Более подробно о запуске тестов можно почитать в
[соответствующем разделе руководства](https://docs.yandex-team.ru/ya-make/usage/ya_make/tests)


#### Примеры запуска тестов:

* Запуск всех интеграционных тестов с детализацией каждого прошедшего теста:
    ```
    ya make -P -tt ~/arcadia/intranet/ims/imscore
    ```

* Запуск всех интеграционных тестов ```Healthz```:
  ```
  ya make -tt -F "ru.yandex.intranet.imscore.grpc.healthz.HealthzTest::*"  ~/arcadia/intranet/ims/imscore
  ```

* Запуск интеграционного теста метода ```Healthz.livenessTest()```:
  ```
  ya make -tt -F "ru.yandex.intranet.imscore.grpc.healthz.HealthzTest::livenessTest()""  ~/arcadia/intranet/ims/imscore
  ```

## Мониторинги:

* [Тестинг дашборд](https://solomon.yandex-team.ru/?project=imscore-testing&dashboard=imscore_testing_dashboard&b=1h&e=)
* [Тестинг postgres](https://yc.yandex-team.ru/folders/akuisn1rkl8e8325v2e9/managed-postgresql/cluster/mdbpohooj8p0bj4flvoi?section=monitoring)
* [Тестинг Deploy](https://deploy.yandex-team.ru/stages/imscore-test/monitoring)
* [Продакшен дашборд](https://solomon.yandex-team.ru/?project=imscore-production&dashboard=imscore_production_dashboard)
* [Продакшен postgres](https://yc.yandex-team.ru/folders/akuisn1rkl8e8325v2e9/managed-postgresql/cluster/mdbhdvc3okttdi10lp0d?section=monitoring)
* [Продакшен Deploy](https://deploy.yandex-team.ru/stages/imscore-prod/monitoring)
