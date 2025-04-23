Деплой серверов осуществляется при помощи Я.Деплой. [Ссылка на проект](https://deploy.yandex-team.ru/projects/market-mbo)

Есть 3 стейджа:

- dev: [dev stage](https://deploy.yandex-team.ru/stages/testing_market_mbo-mdm-dq)
- testing: [testing stage](https://deploy.yandex-team.ru/stages/testing_market_mbo-mdm-dqc)
- production: [prod stage](https://deploy.yandex-team.ru/stages/production_market_mbo-mdm-dqc)

###### Ресурсы для деплоя сервера
- Runtime DQ сервера
    - тип sandbox ресурса: **MARKET_MBO_MDM_DQ**
    - достаточные условия для применения изменений: перезапуск контейнера в Y.Deploy
    - лежит статичным ресурсом в Sandbox, собирается вручную при помощи ya package, для того, чтобы задеплоить необходимо прописать ссылку на ресурс в соответствующем слое deploy unit-а в Я.Деплой ((https://deploy.yandex-team.ru/stages/testing_market_mbo-mdm-dq/config/du-mdm-dqc/box-mdm-dqc_box пример))
- Конфигурация серверов
    - тип ресурса: **MARKET_MBO_MDM_DQ_CONFIG**
    - достаточные условия для применения изменений: перезапуск Runtime DQ сервера
    - лежит в arcadia [тут](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mdm/mdm-dqc/src/main/conf), собирается и деплоится [пайплайном в ЦУМ](https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/dq-plugins)
- Кастомные компоненты LB,YT коннекторы
    - тип ресурса: **MARKET_MBO_MDM_DQ_PLUGIN**
    - достаточные условия для применения изменений: перезапуск Runtime DQ сервера
    - лежит в arcadia [тут](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mdm/mdm-dqc/), собирается и деплоится [пайплайном в ЦУМ](https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/dq-plugins)
- DQD проект(проверки расписания)
    - тип ресурса: **MARKET_MBO_MDM_DQ_WORKFLOW**
    - достаточные условия для применения изменений: перезапуск Runtime DQ сервера
    - лежит в Bitbucket [тут](https://bb.yandex-team.ru/projects/MARKET_MDM/repos/dq), cобирается и деплоится [пайплайном в ЦУМ](https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/dq-plugins)
- Источники данных для DQ
    - тип ресурса: статический ресурс
    - достаточные условия для применения изменений: перезапуск Runtime DQ сервера
    - лежит в YAV прописывается в спеке сервера (e.g ya tool dctl get stage testing_market_mbo-mdm-dq > dev.yaml)
- Слой со SPYT
    - тип ресурса: **PORTO_LAYER_MARKET_MDM_SPYT**
    - достаточные условия для применения изменений: перезапуск контейнера в Y.Deploy
    - скрипт для сборки лежит [тут](https://arcanum.yandex-team.ru/arcadia/market/sre/deploy/porto/layers/spyt/spyt.sh) собирается [таской](https://sandbox.yandex-team.ru/task/1015129277/view)

###### Деплой новой версии runtime сервера от ataccama

1) Скачиваем и распаковываем архив с runtime в директорию <runtime_dir> ![Ataccama runtime](../../_images/dq/dq_deploy_new_version.png)
2) Создаем файл package.json указываем корректную **версию**, и **path**

```json
{
    "meta": {
        "name": "market-mbo-mdm-dq",
        "version": "12.6.3",
        "maintainer": "Sergei Baiborodov <sbye@yandex-team.ru>"
    },
    "data": [
        {
            "source": {
                "type": "RELATIVE",
                "path": "all-runtime-12.6.3",
                "files": [
                    "*"
                ]
            },
            "destination": {
                "path": "/app/dqc/"
            }
        }
    ]
}
```

3) Выполняем
```shell
ya package package.json
```
получаем архив для ресурса sandbox
4) Выгружаем ресурс в sandbox

```shell
ya upload market-mbo-mdm-dq.12.6.3.tar.gz --type MARKET_MBO_MDM_DQ
```

5) Переходим на dev стейдж, нажимаем на кнопку edit ![Редактирование стейджа](../../_images/dq/dq_deploy_stage_edit.png)

Выбираем `mdm-dqc_box` находим слой `MARKET_MBO_MDM_DQ` прописываем id ресурса. ![Редактировани слоя с Runtime](../../_images/dq/dq_deploy_runtime_layer.png)

6) Нажимаем кнопочку update вверху, ждем окончания процесса деплоя, проверяем работоспособность сервера DQ.
7) Если все хорошо можно выполнить пункт 4 с параметром `--ttl inf` и раскатить новый ресурс по всем стейджам dev, prod, testing

###### Деплой DQ проверок

Для деплоя DQ проверок созданы:

- [пайплайн в ЦУМ](https://tsum.yandex-team.ru/pipe/projects/mbo/pipelines/dq-pipelines)
- [релизная машина](https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/dq-pipelines)

Пайплайн забирает файлы проверок и метаданные с master ветки [bitbucket-а](https://bb.yandex-team.ru/projects/MARKET_MDM/repos/dq), пакует и выгружает ресурс в sandbox c типом `MARKET_MBO_MDM_DQ_WORKFLOW` и также прописывает ресурс в соответствующем слое бокса в Я.Деплой.

Альтернативный вариант для деплоя на конкретный env. Использовать напрямую таску `CREATE_RESOURCE_FROM_PLANE_GIT` указать ветку и коммит полученный ID ресурса положить в соотвествующий слой. Например сделать **clone** таски https://sandbox.yandex-team.ru/task/1017888420/view поправить хэш коммита и запустить.

###### Деплой Yandex плагина и конфигов

Для деплоя плагина созданы:

- [пайплайн в ЦУМ](https://tsum.yandex-team.ru/pipe/projects/mbo/pipelines/dq-plugins)
- [релизная машина](https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/dq-plugins)
  Пайплайн собирает 2 ресурса из проекта в [аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbo/mdm/mdm-dqc):
- `MARKET_MBO_MDM_DQ_CONFIG` конфигруации сервера
- `MARKET_MBO_MDM_DQ_PLUGIN` собранная jar-ка плагина и также прописывает ресурсы в соответствующих слоях бокса в Я.Деплой.

Подробнее про разработку плагина: [Разработка yandex plugin](https://docs.yandex-team.ru/market-mdm/development/dq/dq_plugin_development.md)

###### Деплой PORTO слоя со SPYT

Для сборки самого слоя используется таска `BUILD_PORTO_LAYER`, где нужно указать адрес скрипта сборки. Скрипт сборки слоя находится в аркадии https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/deploy/porto/layers/spyt/spyt.sh
Полученный ID ресурса указываем в соответствующем слое `PORTO_LAYER_MARKET_MDM_SPYT` [Пример таски](https://sandbox.yandex-team.ru/task/1015129277/view)

В случае обновления версии SPYT можно:

- просто пересобрать слой и получить последнюю версию поправив [скрипт](https://arcanum.yandex-team.ru/arcadia/market/sre/deploy/porto/layers/spyt/spyt.sh)
```shell
pip install -i https://pypi.yandex-team.ru/simple "yandex-spyt<2.0.0"
```
- либо указать конкретную версию в скрипте
```shell
pip install -i https://pypi.yandex-team.ru/simple "yandex-spyt==1.7.1"
```
###### Правка спецификаций работа с секретами

В Y.Deploy можно работать напрямую со спецификациями в обход UI. Для того чтобы получить спецификацию стейджа конкретного окружения, необходимо воспользоваться утилитой `dctl` подробнее можно почитать тут в т.ч. [как настроить OAuth токен](https://deploy.yandex-team.ru/docs/reference/tools/dctl)

Выгружаем спеку:

- dev: `ya tool dctl get stage testing_market_mbo-mdm-dq > dev.yaml`
- testing: `ya tool dctl get stage testing_market_mbo-mdm-dqc > test.yaml`
- prod: `ya tool dctl get stage production_market_mbo-mdm-dqc > prod.yaml`

Деплоим спеку:
`ya tool dctl put stage spec.yaml`, где **spec.yaml** - исправленная спецификация.

Секреты довозятся через спеку см. [тут](https://deploy.yandex-team.ru/docs/how-to/secrets#kak-zadat-sekrety-cherez-dctl)
