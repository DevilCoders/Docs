# ML Viewer ![](https://img.shields.io/badge/status-dev-blue)

## Домены

**Stable:** [https://ml.logos.yandex-team.ru](https://ml.logos.yandex-team.ru)

**Beta:** [https://beta.ml.logos.yandex-team.ru](https://beta.ml.logos.yandex-team.ru)

## Swagger

**Stable:** [ml.logos.yandex-team.ru/api/docs](https://ml.logos.yandex-team.ru/api/docs)

**Beta:** [beta.ml.logos.yandex-team.ru/api/docs](https://beta.ml.logos.yandex-team.ru/api/docs)

## Deploy environment

**Stable:** [https://deploy.yandex-team.ru/stages/logos-ml-viewer](https://deploy.yandex-team.ru/stages/logos-ml-viewer)

**Beta:** [https://deploy.yandex-team.ru/stages/logos-ml-viewer-beta](https://deploy.yandex-team.ru/stages/logos-ml-viewer-beta)

## The CI

Интерфейс: [https://a.yandex-team.ru/projects/logos/ci/releases/timeline](https://a.yandex-team.ru/projects/logos/ci/releases/timeline?dir=ads%2Femily&id=ml-logos-backend)

Конфигурация: [https://a.yandex-team.ru/arc_vcs/ads/emily/a.yaml](https://a.yandex-team.ru/arc_vcs/ads/emily/a.yaml)

## Как разрабатывать

Получить доступ к [секрету](https://yav.yandex-team.ru/secret/sec-01enabqy9g1d409wjjyx2bnk76).
Тогда все команды будут по умолчанию работать.

Или получить [свой токен](https://oauth.yandex-team.ru/authorize?client_id=cc4bf9db015043edb37506d83862d84b&response_type=token)
и передавать его в `OAUTH_TOKEN`

```bash
# Вытащить текущий state c моделями из qyp на remote машинку
ads/emily/viewer/backend$ make fetch

# Обновить state с помощью препроцессоров из trunk и скачать локально
ads/emily/viewer/backend$ make extract

# Провалидировать state по marshmallow и json схеме
ads/emily/viewer/backend$ make validate

# Скачать stable.json с сандбокса и положить в app/data
ads/emily/viewer/backend$ make download

# Загрузить stable.json из сандбокса в beta
ads/emily/viewer/backend$ make upload

# Запустить backend поверх state c выключенным фетчингом из сандбокса
ads/emily/viewer/backend$ make run
ads/emily/viewer/backend$ make run-dev

# Запустить backend поверх state c включенным фетчингом из сандбокса.
ads/emily/viewer/backend$ NO_DAEMON=0 make run
ads/emily/viewer/backend$ NO_DAEMON=0 make run-dev

# Запустить frontend, который смотрит на локальный backend
ads/emily/viewer/frontend$ make run

# Запустить environment, повторяющий тот, что получится на Qloud
ads/emily/viewer$ make app
```

## Как выкатить stable

Деплой на прод запускается вручную на Sandbox.
В [The CI](https://a.yandex-team.ru/projects/logos/ci/releases/timeline?dir=ads%2Femily&id=ml-logos-backend) перейдите на flow.

![](https://jing.yandex-team.ru/files/dim-gonch/2021-04-16_17-41-44.png)

![](https://jing.yandex-team.ru/files/dim-gonch/2021-04-16_17-43-29.png)

```bash
# Обновляем ревизию кода по генерации state на qyp
# <REVISION> - версия из testenv, на которой запустили деплой BACKEND. В примере - 6539123
ads/emily/viewer/backend$ REVISION=<REVISION> make update
```

Следим за статусом работы stable на [рассылке logos-duty](https://ml.yandex-team.ru/lists/logos-duty).
Оповещения приходят при ошибках (Error) или при смене статуса (Success -> Error, Error -> Success).

## Как обновить stable.json

1. Собрать новую версию `stable.json`

    ```bash
    ads/emily/viewer/backend$ make extract
    ```

2. Загрузить на Sandbox

    ```bash
    ads/emily/viewer/backend$ make upload
    ```

3. Заменить ресурс в файле сборки `backend/ml-backend-pkg.json`

    ```json
    "source": {
        "type": "SANDBOX_RESOURCE",
        "id": 1772213678  <------------
    },
    ```

4. Заменить ресурс в тестах `backend/tests/ya.make`

    ```make
    SET(STABLE_JSON 1772213678)
    ```

5. Заменить ресурс в `backend/Makefile`

    ```make
    SBR ?= 1772213678
    ```

6. Заменить дефолтный ресурс в `backend.app.config.SANDBOX_RESOURCE`

    ```py
    SANDBOX_RESOURCE = int(os.getenv("SANDBOX_RESOURCE", "1772213678"))  <------------
    ```

7. Проверить сборку

    ```bash
    ads/emily/viewer/backend$ make check-package
    ```
