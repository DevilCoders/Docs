Деплой докер-образов
====================

---
> Внимание, деплой образа через BUILD_AND_DEPLOY_CRYPTA_API и release rule - устаревший способ. Актуальный способ - релизить через `common/deploy/create_release` в [новом CI](ci.md).

---

Здесь описаны шаги деплоя приложений Крипты на примере Crypta API. Подробности автосборки описаны в разделе [{#T}](ci.md).

После мержа изменений API и его частей в транк запускается задача в TestEnv — [BUILD_AND_DEPLOY_CRYPTA_API](https://testenv.yandex-team.ru/?screen=job_history&database=crypta&job_name=BUILD_AND_DEPLOY_CRYPTA_API). Соответствующий [yaml-конфиг](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/crypta/api.yaml) задачи лежит в Аркадии.

После этого начнет выполняться сборочная [sandbox-таска](https://sandbox.yandex-team.ru/tasks?children=false&hidden=true&type=CRYPTA_BUILD_AND_RELEASE&tags=TESTENV-JOB-BUILD_AND_DEPLOY_CRYPTA_API&limit=20), которая собирает докер-образ из свежей ревизии Аркадии и заливает его в яндексовый docker-registry (registry.yandex.net).

![sandbox-task-sreenshot](https://jing.yandex-team.ru/files/unretrofied/sandbox_task_example.png)

На данный момент в сборочном конфиге включен автодеплой в тестинг, поэтому специально релизить API в тестинг не нужно. Почти все сервисы Крипты, за редким исключением, разворачиваются в системе Deploy, в проекте [crypta](https://deploy.yandex-team.ru/projects/crypta). Тестинг настроен на стейдже [crypta-api-testing](https://deploy.yandex-team.ru/stages/crypta-api-testing), прод — на стейдже [crypta-api](https://deploy.yandex-team.ru/stages/crypta-api).

Чтобы выкатить контейнер в прод, нужно зарелизить sandbox-таску в **stable**.

![sandbox-release-screenshot](https://jing.yandex-team.ru/files/unretrofied/release_screenshot.png)

## Откат образа/перевыкатка предыдущей версии

Deploy позволяет легко вернуться к предыдущей версии стейджа. Это может пригодится, когда в прод выехало сломанное приложение. На вкладке [History](https://deploy.yandex-team.ru/stages/crypta-api/history) стейджа есть список всех его версий, любую из них можно накатить заново.

Пример на скриншоте: перевыкатка 48-й ревизии. После запуска перевыкатки образ выбранной ревизии выкатится как новая версия, и запустится его деплой.

![stage-versions-history](https://jing.yandex-team.ru/files/unretrofied/rollback.png)
