# Специализированные команды для геосервисов

## `upload-static`

Команда для загрузки статических ресурсов в вашем проекте в карточный s3 бакет.
Загрузка осуществляется через специальную ручку для проксирования в Подрике. Для того, чтобы начать пользоваться это командой необходимо в перменные окружения добавить `STATIC_CLIENT_KEY`, получить вы его можете в [секретнице](https://yav.yandex-team.ru/secret/sec-01cjz2vkw9hqhf3c7skw5g4zxt).

### Базовая конфигурация

```js
{
    "abcServiceName": "maps-test",
    "geoSpecific": {
        "static": [
            {
                "from": "./_/**.*"
            }
        ]
    }
}
```

Поле static ожидает список групп статических файлов.
Каждая группа обязательно должна содержать поле `from`, [glob](https://github.com/isaacs/node-glob) pattern, какие файлы необходимо загрузить (путь отсчитывается от cwd). Итоговый путь будет включать в себя всю сматченную часть from (cwd будет отрезана).

В общем случае, путь будет таким: `https://yastatic.net/s3/front-maps-static/<abcServiceName>/<your_file_path>`.

Например, файл `./_/some.svg` будет доступен по адресу: `https://yastatic.net/s3/front-maps-static/maps-test/_/some.svg`.

### Дополнительные опции

1) Для исключения некоторых файлов из группы, можно воспользоваться полем ignore (принимает массив строк - регулярных выражений).

Например, если передать следующее значение `ignore: ['\\.br$', 'private']`, то из загрузки будут исключены все файлы с расширением `.br` и содержащие строку `private` в пути или названии.

2) Для версионирования статики можно добавлять в путь текущую версию проекта (в qtools конфиге поле registry.tag), для этого в группу файлов необходимо добавить поле `addTag: true`.

Например, если добавить это поле в текущую конфигурацию (предположим registry.tag = 0.0.1), то адрес файла будет на выходе следующий:
`https://yastatic.net/s3/front-maps-static/maps-test/0.0.1/_/some.svg`.


### Типичный конфиг

```js
{
    "registry": {
        "tag": "0.0.1"
        // ...
    },
    "abcServiceName": "maps-test",
    "geoSpecific": {
        "static": [
            {
                "from": "./_/**.*"
            },
            {
                "from": "./build/**/**.*",
                "addTag": true
            }
        ]
    }
}
```

## Monitorings

Все графики и алерты настраиваютсья в `qtools.json`, секция `geoSpecific.monitorings`, тут же указываются мэинтейнеры, те кому будут приходить нотификации

Пример для ключа `geoSpecific.monitorings.components`:
```json
{
    "geoSpecific": {
        "monitorings": {
            "components": [
                {
                    "name": "app",
                    "environment": "production",
                    "groups": {
                        "alerts": {
                            "unispace": {
                                "warn": 75,
                                "crit": 85
                            }
                        },
                        "access-tskv": {
                            "total": {
                                "graph": {
                                    "Not": [
                                        {
                                            "Equals": {
                                                "request_url": "/ping"
                                            }
                                        }
                                    ]
                                },
                                "alerts": {
                                    "vhost-5xx": {
                                        "warn": 1,
                                        "crit": 10
                                    },
                                    "req-timings-75": {
                                        "warn": 80,
                                        "crit": 160
                                    },
                                    "vhost-2xx-trend-down": {
                                        "warn": 10,
                                        "crit": 20
                                    }
                                }
                            }
                        },
                        "app-tskv": {
                            "staStamp-counter": {
                                "Equals": {"group": "staStamp"}
                            },
                            "stvStamp-counter": {
                                "Equals": {"group": "stvStamp"}
                            },
                            "trfStamp-counter": {
                                "Equals": {"group": "trfStamp"}
                            },
                            "meta-counter": {
                                "Equals": {"group": "meta"}
                            },
                            "apikeys-counter": {
                                "Equals": {"group": "apikeys"}
                            },
                            "keyserv-counter": {
                                "Equals": {"group": "keyserv"}
                            }
                        },
                        "alerts-raw": {
                            "custom-signal-alert": {
                                "signal": "<name-of-signal-from-yasm>",
                                "warn": [10, 15],
                                "crit": [15, "None"],
                                "flaps": {
                                    "boost": 0,
                                    "stable": 600,
                                    "critical": 2400
                                }
                            }
                        }
                    }
                }
            ]
        }
    }
}
```
Объект `geoSpecific.monitorings.components[*].groups` может содержать следующие секции:
* `alerts` - это преднастроенные инфраструктурные алерты, по умолчанию они все включены, но можно определить границы crit & warn:
  * `unispace` - алерт на место
  * `cpu-usage`, `cpu-wait`, `cpu-throttled`  - алерт на работу cpu
* `access-tskv` - секция настройки графиков и алертов, по логам nginx
  * `graph` - в этой секции настраиваем рисование графиков [details](https://a.yandex-team.ru/arc/trunk/arcadia/maps/tools/roquefort)
  * `alerts` - Секция настройки алертов, на основе данных с Рокфора
    * `vhost-2xx-drop` - алерт на проседание трафика, задается в абсолютных величанх
    * `vhost-2xx-trend-down` - алерт на проседения трафика, на основе трендов, границы задаются в процентном соотношение
    * `vhost-4xx` - алерт на 4xx коды ошибок, исключая 404, 429 и 499
    * `vhost-429` - алерт строго на 429 коды ошибок
    * `vhost-499` - алерт строго на 499 коды ошибок (timeouts)
    * `vhost-499-high` - алерт строго на 499 коды ошибок, но с маленькой задержкой (1 min)
    * `vhost-5xx` - алерт на все 5xx коды ошибок
    * `vhost-5xx-high` - алерт строго на 5xx коды ошибок, но с маленькой задержкой (1 min)
    * `req-timings-75` - алерт на 75 процентиль тайминогов
    * `req-timings-95` - алерт на 95 процентиль тайминогов
* `alerts-raw` - данная секция позволяет настроить произвольный алерт, на любой сигнал в головане. Подробней [тут](https://github.yandex-team.ru/maps/docker-baseimages/blob/master/flavors/monitorings/README.monitorings.md#%D0%BA%D0%B0%D1%81%D1%82%D0%BE%D0%BC%D0%BD%D1%8B%D0%B5-%D1%81%D0%B8%D0%B3%D0%BD%D0%B0%D0%BB%D1%8B)
    ```json
    {
        "custom-signal-alert": {
            "signal": "<name-of-signal-from-yasm>",
            "warn": [10, 15],
            "crit": [15, "None"],
            "flaps": {
                "boost": 0,
                "stable": 600,
                "critical": 2400
            }
        }
    }
    ```
* `app-tskv` - секция позволяет построить графики на основе логов приложения. Формат аналогичен `access-tskv`:
    ```json
    {
        "app-tskv": {
            "some-counter": {
                "graph": {
                    "Equals": {"group": "some-module"}
                },
                "alerts": {
                    "my-alert": {
                        "warn": 1,
                        "crit": 5
                    }
                }
            }
        }
    }
    ```

    **Note**: Имя проверки обязательно должно заканчиваться на `-counter`.

Пример для ключа `geoSpecific.monitorings.l7`:
```json
{
    "geoSpecific": {
        "monitorings": {
            "l7": [
                {
                    "id": "front-service-slug.slb.maps.yandex.net",
                    "infra": {
                        "cpu-wait": {
                            "warn": 0.4,
                            "crit": 0.5
                        },
                        "cpu-usage": {
                            "warn": 65,
                            "crit": 85
                        },
                        "memory-usage": {
                            "warn": 85,
                            "crit": 95
                        }
                    },
                    "upstreams": {
                        "main": {
                            "inprogress-connection" : {
                                "warn": 25,
                                "crit": 35
                            },
                            "fail-connection" : {
                                "warn": 3,
                                "crit": 5
                            },
                            "connection-timeout" : {
                                "warn": 5,
                                "crit": 6
                            },
                            "backend-timeout" : {
                                "warn": 2,
                                "crit": 4
                            },
                            "connection-refused" : {
                                "warn": 2,
                                "crit": 4
                            },
                            "vhost-5xx" : {
                                "warn": 5,
                                "crit": 7
                            }
                        }
                    }
                }
            ]
        }
    }
}
```
Объект `geoSpecific.monitorings.l7[*]` содержит следующие секции:

* `id` - идентификтор балансера (обычно имеет вид `front-service-slug.slb.maps.yandex.net`), обязательное поле;

* `infra` - описывает инфраструктурные алерты, относящиеся ко всему балансеру в целом:
  * `cpu-usage`, `cpu-wait` - алерты на работу cpu,
  * `memory-usage` - алерт на память.
  
* `upstreams` - описывает алерты для апстримов балансера (обязательное поле):
  * `inprogress-connection` - алерт на количество обрабатываемых в данный момент запросов,
  * `fail-connection` - алерт на количество безуспешно обработанных запросов,
  * `connection-timeout` - алерт на количество таймаутов при попытке установить соединение,
  * `backend-timeout` - алерт на количество таймаутов от приложения,
  * `connection-refused` - алерт на количество отказов в соединении балансеру,
  * `vhost-5xx` - алерт на пятисотки на балансере.

Объект `geoSpecific.monitorings.l7[*].upstreams` должен содержать как минимум один апстрим,
при этом значение ключа может быть пустым объектом. Например, в случае передачи следующего конфига:

```json
{
    "l7": [
        {
            "id": "front-service-slug.slb.maps.yandex.net",
            "upstreams": {
                "main": {}
            }
        }
    ]
}
```
будут выставлены дефолтные границы как для алертов инфраструктуры, так и для алертов апстримов.

## ```alerts <action>```

Команда для создание/обновления/удаления конфига с alert-ами в Golovan.

### Использование

```js
{
    "geoSpecific": {
        "monitorings": {

        }
    }
}
```

```sh
node_modules/.bin/qtools alerts push

node_modules/.bin/qtools alerts remove
```

### ```<action>```

#### ```push```

Команда которая создает конфиг, если он отсутствует в Golovan и обновить, если уже добавлен.

Если удаленный конфиг и новый различаются, команда завершится с кодом 1.
Если удаленный конфиг отсутствует, команда завершится с кодом 1.

Для подтверждения действий создания и обновления конфига, необходимо добавить "--force" к команде.

```sh
node_modules/.bin/qtools alerts push --force
```

#### ```remove```

Команда которая удаляет конфиг.

Для подтверждения действия удаления конфига, необходимо добавить "--force" к команде.

```sh
node_modules/.bin/qtools alerts remove --force
```
