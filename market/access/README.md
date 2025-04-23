# Что это?
Access – это универсальная система публикации (publish) и потребления (consume) файловых ресурсов. Процессы публикации и потребления полностью независимы. Иными словами вы можете опубликовать свой файл через API сервера, а где-то в облаке инстансы вашего сервиса смогут его получить по гибко настраивающимся схемам: все сразу, по очереди со скользящим окном, только подмножество инстансов и т.п. Также поддерживается откат на предыдущую версию для конкретного потребителя. Новые инстансы вашего приложения не требуют конфигурации центрального сервиса, а регистрируются в системе автоматически, ровно как и исчезают при удалении мощностей из системы.

Центральным компонентом системы является Access Server – он накапливает всю информацию об имеющихся в системе ресурсах, их версиях, а также публикаторах, потребителях и их нодах.

Объектная модель Access'a определяет *Resource* как сущность, объединяющую множество *Version*. У Resource есть свой *Publisher*, но идентификация всех ресурсов глобальна и не зависит от имени Publisher'a. *Version* – объект, представляющий конкретный файл или группу файлов, идентифицируется строкой в формате [семантического версионирования](https://semver.org/). Version могут содержать зависимости на версии других ресурсов. На Resource подписываются *Consumer Nodes* – конкретные экземпляры запущенного пользовательского приложения. Конфигурация доставки данных задается через [опции](https://a.yandex-team.ru/arc/trunk/arcadia/market/access/server/proto/consumer.proto) *Consumer*, объединяющего все Consumer Nodes.

Конфигурацией всех объектов системы можно управлять через инструмент [actl](https://a.yandex-team.ru/arc/trunk/arcadia/market/access/actl/bin).

Публикация ресурса может быть организована по push- или pull-модели. В push-модели компонент-публикатор использует [gRPC API](https://a.yandex-team.ru/arc/trunk/arcadia/market/access/server/proto/service.proto) для публикации новых версий. В pull-модели компонент-публикатор просто выкладывает в облако файлы, а для их регистрации в качестве версий используются объекты-puller'ы, созданные через [gRPC API Access Puller](https://a.yandex-team.ru/arc/trunk/arcadia/market/access/puller/proto/service.proto)

Для потребления ресурса в контейнер с пользовательским приложением нужно установить сервис [Access Agent](https://a.yandex-team.ru/arc/trunk/arcadia/market/access/agent/bin), а также слинковать пользовательское приложение с библиотекой [Access Agent Client](https://a.yandex-team.ru/arc/trunk/arcadia/market/access/agent/client).

# Быстрый старт
Все манипуляции для безопасности производятся на тестинге (параметр ```-e test``` ), если необходимо использовать продовое окружение, просто уберите этот параметр. Также можно использовать локально поднятое окружение (см. ниже).
## Публикация ресурса
1. Собираем [actl](https://a.yandex-team.ru/arc/trunk/arcadia/market/access/actl/bin) или используем из PATH
1. Создаем паблишера (если еще нет)
    ```
    $ touch dwarf.txt && <edit> && cat dwarf.txt
    name: "dwarf"
    description: "dwarf from mines"
    $ actl -e test add pub dwarf.txt
    ```
1. Создаем ресурс (если еще нет)
    ```
    $ touch gold.txt && <edit> && cat gold.txt
    name: "gold"
    publisher_name: "dwarf"

    $ actl -e test add res gold.txt
    ```
1. Создаем версию и загружаем в облако (по ссылке 100 байт рандома)
    ```
    $ touch gold-1.0.0.txt && <edit> && cat gold-1.0.0.txt
    resource_name: "gold"
    storage {
        location {
            access {
                rbtorrent: "rbtorrent:0e69830f6d44feaeed0128af569f3990caf2014c"
            }
        }
    }
    $ actl -e test add ver "gold-1.0.0.txt"
    ```
1. Повторяем пп. 3-4 для создания и публикации новых версий

## Потребление ресурса
1. Собираем [access agent](https://a.yandex-team.ru/arc/trunk/arcadia/market/access/agent/bin) и этот [sample](https://a.yandex-team.ru/arc/trunk/arcadia/market/access/sample)
1. Запускаем __access agent__, рабочая директория: ```/tmp/access-sample```
    ```
    $ market/access/agent/bin/bin -c market/access/agent/bin/sample-cfg --env testing --port 2508 --grpc-port 2406 &
    ```
1. Запускаем __sample__
    ```
    $ market/access/sample/sample --agent 2406 --resource "money"
    ```
## Откат версии
1. Откатываемся на прошлую версию
    ```
    $ actl -e test get con sample > sample.txt
    $ <edit> && cat sample.txt
    name: "sample"
    options {
        resource {
            key: "money"
            value {
                update {
                    version: "1.0.0"
                }
            }
        }
    }

    $ actl -e test set con sample.txt
    ```
1. Включаем обновление свежих версий обратно
    ```
    $ actl -e test get con sample > sample.txt
    $ <edit> && cat sample.txt
    name: "sample"

    $ actl -e test set con sample.txt
    ```

## Множественная загрузка версий
1. Разрешаем несколько одновременно установленных версий
    ```
    $ actl -e test get con sample > sample.txt
    $ <edit> && cat sample.txt
    name: "sample"
    resource {
        key: "money"
        value {
            retention {
                install_count: 2
            }
        }
    }

    $ actl -e test set con sample.txt
    ```
1. Публикуем новую версию
    ```
    $ touch gold-2.0.0.txt
    $ <edit> && cat gold-2.0.0.txt
    resource_name: "gold"
    storage {
        location {
            access {
                rbtorrent: "rbtorrent:0e69830f6d44feaeed0128af569f3990caf2014c"
            }
        }
    }
    $ actl -e test add ver "gold-2.0.0.txt"
    ```

## Rolling update
1. Для консюмера устанавливаем настройки download_window и install_window, а также разрешаем раскатку ресурса через rolling deploy
    ```
    $ actl -e test get con sample > sample.txt
    $ <edit> && cat sample.txt
    name: "sample"
    options {
        global {
            update {
                install_window: 2
                download_window: 2
            }
        }

        resource {
            key: "money"
            value {
                update {
                    respect_download_window: true
                    respect_install_window: true
                }
            }
        }
    }

    $ actl -e test set con sample.txt
    ```

1. Следим за раскаткой
    ```
    $ actl -e test list dep sample -a
    ```


## Работа с зависимыми ресурсами
Пусть есть консюмер C1 который должен устанавливать ресурс R1, только после того как консюмер С2 установит ресурс R2.

1. Создаем консюмер группу, для описания связанных консюмеров и ресурсов

    ```
    $ touch group.txt && <edit> && cat group.txt
    id: "my-group"
    resource {
        key: "R1"
        value: "C1"
    }

    resource {
        key: "R2"
        value: "C2"
    }

    $ actl -e test add group group.txt
    ```

1. Версию для R2 публикуем как обычно, при публикации версии для R1 указываем зависимось
    ```
    $ touch r2.txt && <edit> && cat r2.txt
    resource_name: "R2"
    storage {
        location {
            access {
                rbtorrent: "rbtorrent:0e69830f6d44feaeed0128af569f3990caf2014c"
            }
        }
    }
    $ actl -e test add ver r2.txt
    $ touch r1.txt && <edit> && cat r1.txt
    resource_name: "R1"
    storage {
        location {
            access {
                rbtorrent: "rbtorrent:0e69830f6d44feaeed0128af569f3990caf2014c"
            }
        }
    }
    dependency {
        resource_name: "R2"
        version_number: "1.0.0"
    }

    $ actl -e test add ver r1.txt
    ```

1. Следим за ходом раскатки ресурсов
    ```
    $ actl -e test ls gdep my-group -a
    ```

## Локальное окружение
Для ознакомительных и проверочных целей можно поднять локальное окружение следующей командой:
```
$ python <arcadia>/market/access/server/beam/service.py
```

Результат будет выглядеть примерно таким образом:
```
Access
Data:     /dev/shm/yuraaka/access/beam
Http:     localhost:3965
Grpc:     localhost:3966

Ydb
Endpoint: localhost:18609
Database: local
Workdir:  /dev/shm/yuraaka/access/beam/ydb
Tool:     ya ydb -e localhost:18609 -d /local
List:     scheme ls ydb/beam
Read:     table readtable ydb/beam/table
Query:    table query execute -q "PRAGMA TablePathPrefix("/local/ydb/beam"); SELECT * FROM table"
Press ENTER to exit...
```

К локальному окружению можно подключаться через actl для выполнения действий, описанных выше:
```
actl -e localhost:3966 add pub my-pub.txt
```

## Использование снапшотов
Access Agent может работать с локальными файлами и отдавать версии ресурсов без подключения к общему серверу. Это может понадобиться для восстановления рабочего окружения, снятого с production-среды.

Для этого выполните следующее:
1. Скопировать в локальные каталоги с production-окружения файлы стейта агента:
    ```
    * pdata/access-agent/state
    * pdata/access-agent/install
    ```
1. Подготовить конфиг агента:
    ```
    ...
    Installer {
        InstallPath: "<путь-до-локального-install-каталога"
    }

    Messaging {
        StateDir: "<путь-до-локального-state-каталога>/ctl"
        QueueDir: "<путь-до-локального-state-каталога>/queue"
    }

    Consumer {
        ForceLocalCache: true # включаем использование локального кеша
    }
    ...
    ```
1. Запустить ваш ворклод или [sample](https://a.yandex-team.ru/arc/trunk/arcadia/market/access/sample)
    ```
    ./sample --consumer <имя-production-консьюмера> --agent <grpc-порт-запущенного-агента> --resource <имя-ресурса-из-локального-кеша>
    ```
