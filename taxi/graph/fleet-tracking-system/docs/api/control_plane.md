#### Ручки управления конфигурацией

Вопрос об авторизации на доступ к созданию пайплайнов пока оставляем на будущее.

**Настройки пайплайна:**

{% cut 'Пример объекта' %}

```yaml
PipelineSettings:
    version: 3,
    endpoints:
        logbroker_endpoints:
            - name: "my super lb topic 1"
              cluster: lbkx.yandex.team.ru
        mttq_endpoints:
            - name: "some mttq topic"
              endpoint: "mttq.my.company.endpoint"
              credentials: ???
        redis_endpoints:
           - name: "pubsub topic"
             endpoint:
               server: redis.my.company.server
               credentials:
        http_endpoints:
           - name: 
             endpoint:
    streams:
        - name: "production stream"
          protocol: "protocol v1"
          filters:
            - only verified positions
            - discard outdated
          lb_topics: 
             - name: "my super lb topic 1"
          http_callbacks:
              - endpoint: some_endpoint
       - name: all signals stream
         filters:
             - always true
         lb_topics:
            - name "all signals topic"
         protocol: "signals.v7"

         mttq_topic: 
           - name: "some mttq topic"
         redis_pubsub:
           name: "pubsub topic"
```

{% endcut %}

Схемы конфига пайплайна
```yaml
PipelineConfig:
    type: object
    additionalProperties: false
    properties:
        version:
            type: string
        channels-list:
            $ref: "geobus-channel-config/definitions.yaml#/definitions/ChannelList"
        sources-data:
            $ref: "#/definitions/SourcesData"
        input:
            $ref: "#/definitions/InputPipelineConfig"
        yaga:
            $ref: "#/definitions/YagaPipelineConfig"
        yaga-metrolog:
            $ref: "#/definitions/MetrologPipelineConfig"
        trackstory:
            $ref: "#/definitions/TrackstoryPipelineConfig"
    required:
        - channels-list

PipelineConfigList:
    type: object
    additionalProperties:
        $ref: "#/definitions/PipelineConfig"
```

## Версии конфигов

### **Итоговая цель**
В процессе разработки схема конфига будет меняться. Чтобы поддерживать использование пользователями нашего апи, мы будем поддерживать одновременную работу с несколькми версиями конфига (несколькими версиями **схемы** конфига). Помимо новой схемы также будет скрипт для миграции с предыдущей версии до новой, таким образом будет возможность обновлять конфиги с любой версии до любой версии выше изначальной.

#### Клиентская часть (внешнее апи)
Ручки для управления конфигом будут принимать версию в качесве параметра в телеф запроса (он будет являться дискриминатором при парсинге конфига в структуру). Для обновления версии конфига будет специальная ручка миграции, которая под капотом запустит скрипт, после выполнения которого можно будет пользоваться api для новой версии. Новую версию указывает сам пользователь, не обязательно обновляться до последней.

#### Внутренняя часть
Control-plane и сервисы будут поддерживать только последнюю версию конфига. Даже если пользователь хранит и работает с более старой, она будет автоматически апгрейдится на лету до последней и отдаваться сервису именно в таком виде.
Во время обновления схемы сначала будет выкатываться control-plane, поддерживающий новую версию, а затем сервисы, использующие ее. В это время часть сервиов будет хоидть в ручку со старой версией, а часть в ручку с новой версией. После этого преимущества следующей версии будут доступны пользователям.

Конфиги будут храниться в единственном экземпляре - в версии, с которой рабтает пользователь. Уникальным ключом будет являться имя конфига, а версия будет свойством.

#### Последовательность выкатки при добавлении новой конфига
- выкатка control-plane - control-plane будет поддерживать новую врсию при запросе во внутреннюю ручку (которой пользуются сервисы), преобразуя конфиги к новой версии
- выкатка сервисов - сервисы начинают читать новую версию конфига и могут пользоваться нововведениями.

### План на первое время
Пока у нас не так много клиентов, мы можем контролировать использование ими версии нашего апи, заставляя работать с ними через админку. В этом случае не будет необходимости хранить разные версии конфигов и давать возможность пользователям мигрировать самостоятельно. Поэтому первое время мы будем запускать миграцию сами для всех клиентов и обновлять админку в удобное нам время. Публичнng API же не будет принимать версию конфига, а будут начинать работать с новой в тот момент, когда выкатится очередная версия control-plane.
Это упростит написание сервиса, а также увеличит контроль. При этом переход к итоговой цели потребует только небольшого изменения в апи (возмоность указать версию и поддержка нескольких вариантов версий конфига при запросе) и изменения control-plane.

В этом сценарии в базе данных будут храниться несколько конфигов разных версий и сервис сможет отдать любую из них. Уникальной будет пара `(название_конфига, версия)`.

#### Последовательность выкатки при добавлении новой вресии конфига
- выкатка control-plane - перестает работать админка (так как новая схема), в этот момент мы останавливаем изменения конфигов, что позводит нам потом сделать миграцию. Сервисы при этом продоллжают ходить во внутреннюю ручку с предыдущей версией конфигов.
- запускаем миграцию - теперь control-plane будет отдавать пайплайны при запросе во внутреннюю ручку (которой пользуются сервисы)
- выкатка сервисов - теперь сервисы читают новую версию конфига и используют ее
- выкатка админки - теперь пользователи могут менять конфиги, так как схемы в админке будут совпадать со схемой в сервисе


### API
**Создать пайплайн:**
`/v1/config/{pipeline}/create`
```yaml
/v1/config/{pipeline}/create/:
    post:
        description: Создать новый пайплайн.
        requestBody:
            description: Body
            required: true
            content:
                application/json:
                    schema:
                        $ref: '/definitions.yaml#/PipelineSettings'
        responses:
            '200':
                description: Success
            '409':
                description: Пайплайн с таким именем уже существует.
            '400':
                description: Настройки некорректны или нарушенна схема.
                # Чтобы проверить конфиг можно сделать отдельный вызов
```
Аргументы:
   - `PipelineSettings` - конфиг пайплайна
Коды возврата:
   - `200` - если все успешно
   - `409` - если пайплайн существует
   - `400` - если настройки некорректны
   - `400` - если нарушенна схема

{% cut 'Пример' %}

**Успещное создание пустого пайплайна с названием taxi**
- uri: `/v1/config/taxi/create`
- body:
```json
{
    "version" : 3,
    "channels-list": {}
}
```
- response: 200

{% endcut %}

**Проверить настройки без создания пайпланйа**
`/v1/config/validate`
```yaml
/v1/config/validate:
    post:
        description: Returns various positions as requested by user.
        requestBody:
            description: Body
            required: true
            content:
                application/json:
                    schema:
                        $ref: '/definitions.yaml#/PipelineSettings'
        responses:
            '200':
                description: Success. Это относится строго к сетевому сообщению. Успешность
                             верификации схемы определяется содержимым ответа
                content:
                    application/json:
                        schema:
                            type: object
                            properties:
                              is_valid:
                                type: bool
                              errors:
                                # сообщения об ошибках
                                type: array
                                items:
                                  type: object
                                  properties:
                                    code:
                                      type: int
                                      description: Некий код ошибки
                                    message:
                                      type: string
                                      description: Локализованное сообщение об ошибке.

            '400':
                description: Нарушенна схема сообщения
```
Коды возврата
  - `200` - если верификацию удалось запустить. 200 возвращается как в случае если настройки валидны, так и в случае если нет.
  - `400` - если нарушенна схема

Возвращаемые данные:
```yaml
errors:
   - code: любое число а-ля WR5715
   - message: локализированное сообщение об ошибке.
```

{% cut 'Примеры' %}

**Валидация пройдена**
- uri: `/v1/config/validate`
- body:
```json
{
    "version": 2,
    "channels-list": {}
}
```
- response: 200
```json
{
    "is_valid": true,
    "errors": []
}
```

**Валидация не пройдена**
- uri: `/v1/config/validate`
- body:
```json
{
    "version" : 3,
    "channels-list": {},
    "yaga": [
        {
            "input-channel": "positions",
            "adjusted-channel": "adjusted-positions"
        }
    ]
}
```
- response: 200
```json
{
    "is_valid": false,
    "errors": [
        {
            "code": 1,
            "message": "No channel 'positions' in channel-list"
        },
        {
            "code": 1,
            "message": "No channel 'adjusted-positions' in channel-list"
        }
    ]
}
```

{% endcut %}

**Изменение пайплайна**
`/v1/config/{pipeline}/edit`
```yaml
/v1/config/{pipeline}/edit:
    post:
        description: Установить новые настройки пайплайна
        requestBody:
            description: Body
            required: true
            content:
                application/json:
                    schema:
                        type: object
                        properties:
                            old:
                                $ref: '/definitions.yaml#/PipelineSettings'
                            new:
                                $ref: '/definitions.yaml#/PipelineSettings'
        responses:
            '200':
                description: Success
            '400':
                description: Настройки некорректны или нарушенна схема.
                # Чтобы проверить конфиг можно сделать отдельный вызов
```
Аргументы:
   - `old`: старое значение конфига
   - `new`: новое значение конфига
Коды возврата:
   - `200` - если все успешно
   - `400` - если настройки некорректны
   - `400` - если нарушенна схема

Для успешного изменения значения `old` должен совпадать с актуальным значением конфига в базе данных. Это позволяет избежать проблем при одновременном изменении значения несколькими пользователями.
Мы выбрали такую схему вместо использования, например, etag, т.к. эта схема уже
поддержанна в нашей админке и это позволит нам иметь удобный интерфейс за 2-3
дня разработки, а не месяц.

{% cut 'Пример' %}

**Изменить значение конфига для пайплайна taxi**

- uri: `/v1/config/taxi/edit`
- body:`
```json
{
    "old": {
        "version" : 3,
        "channels-list": {}
    },
    "new": {
        "version" : 3,
        "channels-list": {
            "positions": {
                "address": "channel:taxi:positions",
                "protocol": "positions",
                "type": "positions",
                "redis-name": "taxi-passing",
                "partitions": 6
            }
        }
    }
}
```
- response: 200

{% endcut %}
 
**Проверить статус пайплайна**
`pipeline/{pipeline_name}/check`
Проверяет что все каналы доступны, все работает. Возвращает статистику. Метод можно вызывать над выключенным пайплайном. Метод проверяет доступность стримов.
```yaml
sinks:
   - name: (имя из настроек)
     status: BAD (OK или BAD)
     error_msg: Не удалось подключится к mttq endpoint. Ошибка: 
   - name: повторять до упора
 
quotas:
   - service: "притягиватель"
     quota:
           percent: 50
           quota_points: 45000
           limit: 60000
   - service: прием координат
     quota:
         

 
statistics:
   - TDB: вообще тут нужно возвращать статистику, но это не ручка для отслеживания рантайм статитстики. Скорее что-то а-ля дневное. За день столько-то и столько-то.
```

**Включение/выключение**
Это как удаление, только настройки остаются жить у нас.
pipeline/enable/{pipeline_name}
pipeline/disable/{pipeline_name}
```yaml
/pipeline/{pipeline}/enable:
    get:
        description: Включить/выключить пайплайн
        responses:
            '200':
                description: Success
            '400':
                description: нарушение схемы
            '404':
                description: нет такого пайплайна
```

**Удалить пайплайн**:
`/v1/config/{pipeline}/delete`
```yaml
/v1/config/{pipeline}/delete:
    post:
        description: Включить/выключить пайплайн
        responses:
            '200':
                description: Success
            '400':
                description: нарушение схемы
            '404':
                description: нет такого пайплайна
```

{% cut 'Пример' %}

**Успешное удаление пайплайна taxi**

- uri: `/v1/config/taxi/delete`
- body: `{}`
- response: 200

{% endcut %}

**Список активных пайплайнов**
`/v1/config/list`
```yaml
/v1/config/list:
    get:
        description: Вернуть список всех пайплайнов
        responses:
            '200':
                description: Success
                content:
                    application/json:
                        schema:
                            type: object
                            properties:
                              name:
                                type: string
                            required:
                              - name
```

{% cut 'Пример' %}

**Получение списка существующих пайплайнов**
- uri: `/v1/config/list`
- body: {}
- response: 200,
```json
[
    "camera",
    "carsharing",
    "taxi"
]
```

{% endcut %}

**Получить значение конфига конкретного пайплайна**
`/v1/config/{pipeline}/get`
```yaml
/v1/config/{pipeline}/get:
    get:
        description: Получить значение конфига пайплайна pipeline
        responses:
            '200':
                description: Success
                content:
                    application/json:
                        schema:
                            $ref: '/definitions.yaml#/PipelineSettings'
            '404':
                description: Пайплайн не найден

```

{% cut 'Пример' %}

**Получить значение конфига пайплайна taxi**
- uri: `/v1/config/taxi/get`
- body: {}
- response: 200,
```json
{
    "channels-list": {
        "positions": {
            "address": "channel:taxi:positions",
            "protocol": "positions",
            "type": "positions",
            "redis-name": "taxi-passing",
            "partitions": 6
        }
    }
}
```

{% endcut %}

**Получить значения всех конфигов**
`/internal/config/v2/get-all/`
Внутренняя ручка, которой пользуются сервисы для получения актуальных настроек пайплайнов
Это решение не годится когда пайплайнов станет много, но сейчас нет смысла
тратить ресурсы на разработку пагинации или другой механизм подписки.
Сервис в query передает ту версию конфига, которую он готов поддерживать. Она
будет отличаться от самой свежей только в момент релизов, когда еще не все
сервисы зарелизились.
```yaml
/internal/config/v2/get-all/:
    get:
        description: Получить значение конфига пайплайна pipeline
        responses:
            '200':
                description: Success
                content:
                    application/json:
                        schema:
                            $ref: '/definitions.yaml#/PipelineSettingsList'
```

{% cut 'Пример' %}

**Получение значения конфигов для всех пайплайнов**
- uri: `/internal/config/v2/get-all/?version=3`
- body: {}
- response: 200,
```json
{
    "taxi:" {
        "channels-list": {
            "positions": {
                "address": "channel:taxi:positions",
                "protocol": "positions",
                "type": "positions",
                "redis-name": "taxi-passing",
                "partitions": 6
            }
        }
    },
    "camera": {
        "channels-list": {
            "positions": {
                "address": "channel:camera:positions",
                "protocol": "positions",
                "type": "positions",
                "redis-name": "taxi-passing",
                "partitions": 6
            },
            "adjusted-positions": {
                "address": "channel:camera:adjusted-positions",
                "protocol": "edge",
                "type": "adjusted",
                "redis-name": "taxi-passing",
                "partitions": 6
            }
        }
    }
}
```

{% endcut %}

