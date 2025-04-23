# Предложение по обновлению прошивок

## Введение
В рамках подключения Яндекс.Драйва как нового источника данных для "Зеркал" было разработано
начальное решение для безопасного обновления прошивок на мобильных агентах. Данный документ
описывает предложения по улучшению и обобщению этого решения для его использования в других
похожих проектах. Решение может быть применено в проектах, где требуется надежное обновление
прошивки на встроенном устройстве по воздуху в отсутствие физического доступа к устройству.

Документ описывает обновление прошивок, реализованное в виде полного обновление дисковых разделов.
Документ НЕ описывает обновление отдельных программных компонентов (напр. отдельных пакетов).

## Требования к решению
1. Каждое клиентское устройство должно уметь самостоятельно обновлять прошивку в течение своей работы.
2. В случае неуспешного обновления (невозможность загрузиться с установленной прошивкой) устройство
должно автоматически откатываться на предыдущую рабочую прошивку.
3. Поддерживать более одного типа устройств (производитель/платформа/архитектура/...).
4. Поддерживать ветки окружения: `testing`, `stable`, ...
5. Поддерживать раскатку на процент устройств.
6. Должен быть реализован бекенд для управления прошивками с поддержкой прав доступа.

## Основные архитектурные решения
1. Точкой входа клиентских устройств является публичный сервер обновлений `Updater`.
Адрес endpoint-а сервиса обновлений содержится внутри прошивки.
2. Точкой входа пользователя для управления раскатками прошивок является внутренний бекенд `Storage`
с https- и cli-интерфейсами. Авторизация пользователя выполняется с помощью TVM-токена (при взаимодействии по https)
и с помощью ssh-ключа при работе через  cli.
3. Разграничение доступа пользователей к системе управления раскатками реализуется посредством idm.
4. Единицей обновления является образ дискового раздела.
5. Разделы, подлежащие обновлению, присутствуют на устройстве в (1+1)-дублированной схеме (active + inactive).
Для безопасного обновления и переключения разделов используется [RAUC](https://rauc.io/).
6. Для хранения прошивок используется бакет в S3.
![image](https://jing.yandex-team.ru/files/miplot/mrc-drive-updater-4.png)

## Реализация
### Серверная часть
#### Модель данных
Зарегистрированные в системе прошивки будeт иметь следующий набор атрибутов:
- `hardware` — уникальное в рамках всей системы наименование устройства (`mrc-nanopi-neo4`, `mrc--raspberry-pi-3b`, ...),
- `slot` — тип дискового раздела, для которого предназначено обновление (`rootfs`, `appfs`, `bootloader`, ...),
- `version` — версия прошивки.

Диапазон устройств, на который должна быть установлена данная прошивка будем называть `scope`.
Он определяется комбинацией параметров (`hardware`, `branch`), а также идентификатором устройства
`deviceid` в случае раскатки экспериментов на процент.

Каждое устройство имеет уникальный идентификатор: `deviceid`. При обновлении устройство будет
присылать в параметрах запроса свой `deviceid` и `hardware`. Сервером будет определяться, к какому
окружению  — `branch` — относится данное устройство на основе его `deviceid`. `branch` может принимать
значения `stable` | `testing` | ... .

Downgrade версии прошивки -- это в общем случае довольно опасная операция, ее очень сложно выполнить корректно и безопасно, потому что
не достаточно откатить только версию прошивки, необходимо также поддержать downgrade на уровне хранимых данных, а это значит, что все приложения,
хранящие данные в постоянной памяти, должны быть backward и forward-совместимы по данным. Этого добиться очень сложно, поэтому принято решение защититься от
downgrade на уровне сервера обновлений. Мы стараемся избежать ситуации, когда на запрос о текущей целевой версии клиенту придет версия, предшествующая
той, что установлена на клиенте.

Для хранения информации о прошивках и правилах раскатки будут использоваться следующие таблицы.


##### firmware_upload

Содержит информацию об активных загрузках прошивок.

| field | type |
|-------|------|
| id | bigint |
| hardware_id | string references(hardware.id)|
| slot | enum string |
| version | string |
| created_at | date |
| created_by | string |

##### firmware_upload_part

| field | type |
|-------|------|
| id | bigint |
| firmware_upload_id | bigint references(firmware_upload.id)|
| content_size | bigint |
| content_md5 | string |

##### hardware

Содержит идентификатор и описание hardware-конфигурации конкретного устройства.
В атрибутах могут храниться специфичные для проекта атрибуты, такие как `name`, `manufacturer`, `architecture`, и т.д.

| field | type |
|-------|------|
| id | string |
| attrs | jsonb |

##### firmware

Содержит метаданные версий прошивок и ссылки для скачивания.

| field | type |
|------|------|
| id | bigint |
| hardware_id | string references(hardware.id)|
| slot | enum string |
| version | string |
| version_seq | bigint |
| url | string |
| size | bigint |
| md5 | string |

Unique constraint (hardware_id, slot, version)
Unique constraint (hardware_id, slot, version_seq)

Записи в таблице нельзя изменять после их добавления.
Для упорядочивания версий прошивок мы будем использовать поле `firmware.version_seq`, оно будет автоматически формироваться из автоинкрементирующейся последовательности при заливке новой прошивки.

##### firmware_rollout

Содержит реестр раскаток.

| field | type |
|-------|------|
| id | (immutable) bigint |
| branch | (immutable) enum string |
| firmware_id | (immutable) bigint references(firmware.id) |
| seed | string |


Поле `id` в `firmware_rollout` используется для хронологического упорядочивания раскаток.
Записи в этой таблице также являются неизменными, разрешается только добавление.

Чтобы обеспечить гарантию о недопущении downgrade прошивок на клиенте, при добавлении записей в `firmware_rollout` должно проверяться следующее ограничение: `firmware.version_seq` должна строго расти в пределах `firmware.hardware, firmware.slot, branch`. Наиболее надежный способ это гарантировать -- это
создать `AFTER INSERT TRIGGER` на таблице `firmware_rollout`.


##### firmware_rollout_history

Хранит историю изменения состояния раскаток.

| field | type |
|-------|------|
| id | bigint |
| rollout_id | bigint references(firmware_rollout.id)
| percent | smallint |
| status | enum |
| created_at | date |
| created_by | string |

Поле `id` используется для хронологического упорядочивания изменения состояния прошивок.
Записи в таблице `firmware_rollout_history` также являются неизменными, их можно только добавлять.

Чтобы обеспечить гарантию о недопущении downgrade прошивок на клиенте, при добавлении записей в `firmware_rollout_history` необходимо гарантировать:
1) нельзя иметь более одного активного эксперимента, то есть нельзя добавить в `firmware_rollout_history`
запись со `status='active' && percent < 100`,  если у первой записи в firmware_rollout_history для данных
`rollout.firmware.hardware, rollout.firmware.slot, rollout.branch` и со `status='active'` выполняется условие
`percent < 100`.
2) нельзя уменьшать процент, нельзя добавить запись, если у добавляемой записи `percent` меньше, чем у дргой записи с тем же `rollout_id`.
3) нельзя модифицировать раскатку "из прошлого": у добавляемой записи `rollout_id` должна быть `>= max(rollout_id)` для данных `rollout.firmware.hardware, rollout.firmware.slot, rollout.branch` и со `status='active'`.
Эти условия также лучше проверять ну уровне `AFTER INSERT TRIGGER` на таблице `firmware_rollout_history`.

##### branch

Хранит список доступных веток.

| field | type |
|-------|------|
| branch | string |

##### device_branch

Хранит принадлежность конкретного устройства к окружению. По-уполчанию устройства относятся к `stable`.
| field | type |
|-------|------|
| hardware_id | string |
| deviceid | string |
| branch_id | string references(branch.id) |

`Unique constraint (hardware_id, deviceid).`

#### Storage API
Сервис будет доступен через внутренний балансер по fqdn `core-firmware-storage.maps.yandex.net`.
Все запросы к API Storage должны содержать TVM-тикет.

##### PUT /v2/firmware/upload/start
Инициирует загрузку прошивки. В параметрах запроса должны быть указаны атрибуты прошивки.

| **Method** | PUT |
|------------|-----|
| **Parameters** |
| hardware | device hardware, e.g. `mrc-nanopi-neo4` |
| slot |  name of the slot this firmware created for |
| version | firmware version |
| **Request Headers** |
| Accept | application/protobuf |
| X-Ya-User-Ticket | TVM ticket |
| **Response codes** |
| 201 | Created |
| 400 | Wrong parameter value |
| 401 | Unauthorized |
| 403 | Permission denied |
| 409 | Conflict |
| **Response Headers** |
| Content-Type | application/protobuf |
| **Response body** |
| Information about created upload |

**Response body**
```c++
Upload {
    id: "12345",
    hardware: "mrc-nanopi-neo4",
    slot: "rootfs",
    version: "1.0.1-1"
}
```

##### PUT /v2/firmware/upload/add_part
Загружает фрагмент данных.

| **Method** | PUT |
|------------|-----|
| **Parameters** |
| id | upload id |
| part | part id |
| **Request Headers** |
| Accept | application/protobuf |
| X-Ya-User-Ticket | TVM ticket |
| Content-Length | Size of part in bytes |
| Content-MD5 | MD5-sum for part content |
| **Response codes** |
| 200 | Ok |
| 400 | Wrong parameter value |
| 401 | Unauthorized |
| 403 | Permission denied |
| **Response Headers** |
| Content-Type | application/protobuf |
| **Response body** |
| Information about uploaded part |

**Response body**
```c++
UploadPart {
    upload_id: "12345",
    part_id: "1",
    content_size: 2156042,
    content_md5: "53f31a089339194f333d2e3995dbb05e"
}
```

##### POST /v2/firmware/upload/finish
Завершает загрузку. В теле запроса должны быть перечислены part_id, content_md5 для всех фрагментов.

| **Method** | POST |
|------------|-----|
| **Parameters** |
| id | upload id |
| **Request Headers** |
| Accept | application/protobuf |
| X-Ya-User-Ticket | TVM ticket |
| **Response codes** |
| 200 | Ok |
| 400 | Wrong parameter value |
| 401 | Unauthorized |
| 403 | Permission denied |
| **Response Headers** |
| Content-Type | application/protobuf |
| **Response body** |
| Information about uploaded part |

**Request body**
```c++
[
    UploadPart {
        upload_id: "12345",
        part_id: "1",
        content_size: 2156042,
        content_md5: "53f31a089339194f333d2e3995dbb05e"
    },
    UploadPart {
        upload_id: "12345",
        part_id: "2",
        content_size: 2156042,
        content_md5: "c0620bbde4d9c45388abf127adc2b01b"
    }
]
```

**Response body**
```c++
Firmware {
    hardware: "mrc-nanopi-neo4",
    slot: "rootfs",
    version: "1.0.1-1",
    version_seq: 123,
    download_url: "http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4a2ede78e6f59c56f19548886ca6070d"
    content_md5: "53f31a089339194f333d2e3995dbb05e",
    content_size: 4312084
}
```

##### GET /v2/firmware/upload/list
Получает информацию об активных загрузках.

| **Method** | GET |
|------------|-----|
| **Parameters** |
| results | show `n` results |
| skip | skip `n` results |
| **Request Headers** |
| Accept | application/protobuf |
| X-Ya-User-Ticket | TVM ticket |
| **Response codes** |
| 200 | Ok |
| 401 | Unauthorized |
| 403 | Permission denied |
| **Response Headers** |
| Content-Type | application/protobuf |
| **Response body** |
| Information about created uploads |

**Response body**
```c++
[
    Upload {
        id: "12345",
        created_at: 1590483573,
        created_by: quoter,
        parts:[
            UploadPart {
                upload_id: "12345",
                part_id: "1",
                content_size: 2156042,
                content_md5: "53f31a089339194f333d2e3995dbb05e"
            },
            ...
        ]
    },
    ...
]
```

##### DELETE /v2/firmware/upload/delete
Удаляет загрузку.

| **Method** | DELETE |
|------------|-----|
| **Parameters** |
| id | upload id |
| **Request Headers** |
| Accept | application/protobuf |
| X-Ya-User-Ticket | TVM ticket |
| **Response codes** |
| 200 | Ok |
| 400 | Wrong parameter value |
| 401 | Unauthorized |
| 403 | Permission denied |



##### GET /v2/firmware/list
Возвращает список зарегистрированных прошивок.

| **Method** | GET |
|------------|-----|
| **Parameters** |
| hardware | (optional) device hardware, e.g. `mrc-nanopi-neo4` |
| slot | (optional) name of the slot this firmware created for |
| results | show `n` results |
| skip | skip `n` results |
| **Request Headers** |
| Accept | application/protobuf |
| X-Ya-User-Ticket | TVM ticket |
| **Response codes** |
| 200 | OK |
| 400 | Bad request, firmware was not found in s3 |
| 401 | Unauthorized |
| 403 | Permission denied |
| **Response Headers** |
| Content-Type | application/protobuf |
| **Response body** |
| Information about registered firmwares |

**Response body**
```c++
[
    Firmware {
        hardware: "mrc-nanopi-neo4",
        slot: "rootfs",
        version_seq: 123,
        version: "1.0.1-1",
        download_url: "http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4a2ede78e6f59c56f19548886ca6070d",
        content_md5: "53f31a089339194f333d2e3995dbb05e",
        content_size: 4312084
    },
    ...
]
```

##### DELETE /v2/firmware/delete
Удаляет прошивку из хранилища.

| **Method** | DELETE |
|------------|-----|
| **Parameters** |
| hardware |  device hardware, e.g. `mrc-nanopi-neo4` |
| slot |  name of the slot this firmware created for |
| version | firmware version |
| **Request Headers** |
| Accept | application/protobuf |
| X-Ya-User-Ticket | TVM ticket |
| **Response codes** |
| 200 | OK |
| 400 | Bad request|
| 401 | Unauthorized |
| 403 | Permission denied |
| 404 | Firmware was not found |
| 424 | Failed dependency, there is a rollout referencing this firmware |


##### POST /v2/rollout/create
 Создает новую раскатку, возвращает ее идентификатор.

| **Method** | POST |
|------------|-----|
| **Parameters** |
| hardware | device hardware, e.g. `mrc-nanopi-neo4` |
| slot | name of the slot this firmware created for |
| branch | `stable` or `testing` |
| version | target firmware version |
| **Request Headers** |
| Accept | application/protobuf |
| X-Ya-User-Ticket | TVM ticket |
| **Response codes** |
| 200 | OK |
| 400 | Bad request|
| 401 | Unauthorized |
| 403 | Permission denied |
| 409 | Conflict |
| **Response Headers** |
| Content-Type | application/protobuf |
| **Response body** |
| Information about registered firmware |

**Response body**
```c++
Rollout {
    id: 123,
    branch: "stable",
    percent: 0,
    status: "inactive",
    firmware: {
        hardware: "mrc-nanopi-neo4",
        slot: "rootfs",
        version_seq: 123,
        version: "1.0.0-1",
        download_url: "http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4ccbe11d031968d5c4297d0eec769b9a"
        content_md5: "4ccbe11d031968d5c4297d0eec769b9a",
        content_size: 4312000,
        created_at: 1596462287200,
        created_by: "miplot"
    }
}
```

Обработка запроса:
1) проверить, что существует `firmware` с соответствующими `hardware_id, slot, version`, иначе -- вернуть `400 Bad request`.
2) Вычислить `seed` для `rollout`: если последняя раскатка для этого scope раскачена на 100% и активна, сгенерировать новый `seed`, в противном случае -- использовать `seed` последней раскатки.
3) Посредством триггера на базе проверить, что `firmware.version_seq` строго растет в пределах `firmware.hardware, firmware.slot, branch`, в противном случае вернуть `400 Bad request`.
4) создать новые записи в `firmware_rollout`, `firmware_rollout_history` c `percent=0, status='inactive'`.


##### POST /v2/rollout/expand
Расширяет процент раскатки, активирует ее.

| **Method** | POST |
|------------|-----|
| **Parameters** |
| rollout_id |  |
| percent | int in range [1, 100] |
| **Request Headers** |
| Accept | application/protobuf |
| X-Ya-User-Ticket | TVM ticket |
| **Response codes** |
| 200 | OK |
| 400 | Bad request|
| 401 | Unauthorized |
| 403 | Permission denied |
| 404 | Not found |
| 409 | Conflict |
| **Response Headers** |
| Content-Type | application/protobuf |
| **Response body** |
| Information about registered firmware |

**Response body**
```c++
Rollout {
    id: 123,
    branch: "stable",
    percent: 10,
    status: "active",
    firmware {
        hardware: "mrc-nanopi-neo4",
        slot: "rootfs",
        version_seq: 123,
        version: "1.0.0-1",
        download_url: "http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4ccbe11d031968d5c4297d0eec769b9a"
        content_md5: "4ccbe11d031968d5c4297d0eec769b9a",
        content_size: 4312000,
        created_at: 1596462287200,
        created_by: "miplot"
    }
}
```

Обработка запроса:
1) проверить, что соответствующая раскатка существует, иначе -- вернуть `404 Not found`
2) попытаться добавить в `firmware_rollout_history` запись с соответствующим `percent` и `status='active'`. Если нарушится ограничение целостности данных -- вернуть `400 Bad request`.


##### POST /v2/rollout/pause
Приостанавливает раскатку.

| **Method** | POST |
|------------|-----|
| **Parameters** |
| rollout_id |  |
| **Request Headers** |
| Accept | application/protobuf |
| X-Ya-User-Ticket | TVM ticket |
| **Response codes** |
| 200 | OK |
| 400 | Bad request|
| 401 | Unauthorized |
| 403 | Permission denied |
| 404 | Not found |
| 409 | Conflict |
| **Response Headers** |
| Content-Type | application/protobuf |
| **Response body** |
| Information about registered firmware |

**Response body**
```c++
Rollout {
    id: 123,
    branch: "stable",
    percent: 10,
    status: "inactive",
    firmware {
        hardware: "mrc-nanopi-neo4",
        slot: "rootfs",
        version_seq: 123,
        version: "1.0.0-1",
        download_url: "http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4ccbe11d031968d5c4297d0eec769b9a"
        content_md5: "4ccbe11d031968d5c4297d0eec769b9a",
        content_size: 4312000,
        created_at: 1596462287200,
        created_by: "miplot"
    }
}
```

Обработка запроса:
1) проверить, что соответствующая раскатка существует, иначе -- вернуть `404 Not found`
2) попытаться добавить в `firmware_rollout_history` запись с  `status='inactive'`. Если нарушится ограничение целостности данных -- вернуть `400 Bad request`.


##### POST /v2/rollout/resume
Возобновляет раскатку.

| **Method** | POST |
|------------|-----|
| **Parameters** |
| rollout_id |  |
| **Request Headers** |
| Accept | application/protobuf |
| X-Ya-User-Ticket | TVM ticket |
| **Response codes** |
| 200 | OK |
| 400 | Bad request|
| 401 | Unauthorized |
| 403 | Permission denied |
| 404 | Not found |
| 409 | Conflict |
| **Response Headers** |
| Content-Type | application/protobuf |
| **Response body** |
| Information about registered firmware |

**Response body**
```c++
Rollout {
    id: 123,
    branch: "stable",
    percent: 10,
    status: "active",
    firmware {
        hardware: "mrc-nanopi-neo4",
        slot: "rootfs",
        version_seq: 123,
        version: "1.0.0-1",
        download_url: "http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4ccbe11d031968d5c4297d0eec769b9a"
        content_md5: "4ccbe11d031968d5c4297d0eec769b9a",
        content_size: 4312000,
        created_at: 1596462287200,
        created_by: "miplot"
    }
}
```

Обработка запроса:
1) проверить, что соответствующая раскатка существует, иначе -- вернуть `404 Not found`
2) попытаться добавить в `firmware_rollout_history` запись с `status='active'`. Если нарушится ограничение целостности данных -- вернуть `400 Bad request`.


##### GET /v2/rollout/target
Выдает информацию о целевом состоянии прошивок.

| **Method** |  GET |
|------------|-----|
| **Parameters** |
| hardware | device hardware, e.g. `mrc-nanopi-neo4` |
| slot | (optional) name of the slot this firmware created for |
| branch | (optional) `stable` or `testing`|
| **Request Headers** |
| Accept | application/protobuf |
| X-Ya-User-Ticket | TVM ticket |
| **Response codes** |
| 200 | OK |
| 400 | Bad request|
| 401 | Unauthorized |
| 403 | Permission denied |
| **Response Headers** |
| Content-Type | application/protobuf |
| **Response body** |
| Information about registered firmware |


##### GET /v2/rollout/history
Выдает информацию об изменении целевых состояний прошивок.

| **Method** |  GET |
|------------|-----|
| **Parameters** |
| hardware | device hardware, e.g. `mrc-nanopi-neo4` |
| slot | (optional) name of the slot this firmware created for |
| branch | (optional) `stable` or `testing`|
| results | (optional) show `n` results |
| skip | (optional) skip `n` results |
| **Request Headers** |
| Accept | application/protobuf |
| X-Ya-User-Ticket | TVM ticket |
| **Response codes** |
| 200 | OK |
| 400 | Bad request|
| 401 | Unauthorized |
| 403 | Permission denied |
| **Response Headers** |
| Content-Type | application/protobuf |
| **Response body** |
| Information about registered rollouts in chronological order from the newest|
**Response body**
```c++
[
    Rollout {
        id: 123,
        branch: "stable",
        percent: 0,
        status: "inactive",
        firmware {
            hardware: "mrc-nanopi-neo4",
            slot: "rootfs",
            version_seq: 123,
            version: "1.0.0-1",
            download_url: "http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4ccbe11d031968d5c4297d0eec769b9a"
            content_md5: "4ccbe11d031968d5c4297d0eec769b9a",
            content_size: 4312000,
            created_at: 1596462287200,
            created_by: "miplot"
        }
    },
    ...
}
```


##### POST /v2/branch/add_device
Привязывает устройство к `branch`.

| **Method** | POST |
|------------|-----|
| **Parameters** |
| hardware | device hardware, e.g. `mrc-nanopi-neo4` |
| deviceid | device identifier |
| branch | branch, e.g. `testing` or `stable` |
| **Request Headers** |
| Accept | application/protobuf |
| X-Ya-User-Ticket | TVM ticket |
| **Response codes** |
| 200 | OK |
| 400 | Bad request, firmware was not found in s3 |
| 401 | Unauthorized |
| 403 | Permission denied |
| **Response Headers** |
| Content-Type | application/protobuf |
| **Response body** |
| Information about registered device |

**Response body**
```c++
{
    hardware: "mrc-nanopi-neo4",
    deviceid: "1234678326478",
    branch: "testing"
}
```

##### GET /v2/branch/list_devices
Возвращает список привязанных к данному `branch` устройств.

| **Method** | GET |
|------------|-----|
| **Parameters** |
| hardware | device hardware, e.g. `mrc-nanopi-neo4` |
| deviceid | (optional) device identifier |
| branch | (optional) branch, e.g. `testing` or `stable` |
| results | show `n` results |
| skip | skip `n` results |
| **Request Headers** |
| Accept | application/protobuf |
| X-Ya-User-Ticket | TVM ticket |
| **Response codes** |
| 200 | OK |
| 400 | Bad request, firmware was not found in s3 |
| 401 | Unauthorized |
| 403 | Permission denied |
| **Response Headers** |
| Content-Type | application/protobuf |
| **Response body** |
| Information about registered firmwares |

**Response body**
```c++
[
    {
        hardware: "mrc-nanopi-neo4",
        deviceid: 1234678326478,
        branch: "testing"
    },
    ...
]
```

##### DELETE /v2/branch/remove_device
Удаляет привязку устройства.

| **Method** | DELETE |
|------------|-----|
| **Parameters** |
| hardware | device hardware, e.g. `mrc-nanopi-neo4` |
| deviceid | device identifier |
| **Request Headers** |
| Accept | application/protobuf |
| X-Ya-User-Ticket | TVM ticket |
| **Response codes** |
| 200 | OK |
| 400 | Bad request|
| 401 | Unauthorized |
| 403 | Permission denied |


#### Updater API

Предлагается отдавать ответ в json, а не protobuf, т.к. ответ будет парситься скриптами, которым проще работать с текстовым, а не бинарным форматом. Сервис будет доступен верез внешний балансер по fqdn `core-firmware-updater.maps.yandex.net`.

##### GET /firmware/1.x/target_state

Запрашивает актуальную версию прошивки. Ответ содержит целевое состояние для данного устройства.
| **Method** | GET |
|------------|-----|
| **Parameters** |
| hardware | device hardware, e.g. `mrc-nanopi-neo4` |
| deviceid | device identifier |
| slots | comma-separated list of updatable slots on device |
| **Request Headers** |
| Accept | application/json |
| X-YFirmware-Signature | request signature |
| User-Agent | Contains whitespace-separated installed firmware versions in format `mrc-nanopi-neo4-rootfs/2020.04.01 mrc-nanopi-neo4-appfs/2020.06.10` |
| **Response codes** |
| 200 | OK |
| 204 | No Content. Could not determine target state for device. Device should keep its current state |
| 400 | Bad request |
| 404 | Not found |
| **Response Headers** |
| Content-Type | application/json |
| **Response body** |
| Information about the target firmware state to be installed |

**Response body**
```json
{
    "slots" : [
        {
            "name": "rootfs",
            "version": "2020.04.01",
            "url": "http://s3.yandex.net/maps-mrc-drive-package/mrc-nanopi-neo4-rootfs-2020.04.01-arm64.raucb",
            "md5": "54230f6a78a50012dd9c2a8d6d9a21ef",
            "size": 378702014
        },
        {
            "name": "appfs",
            "version": "2020.05.15",
            "url": "http://s3.yandex.net/maps-mrc-drive-package/mrc-nanopi-neo4-appfs-2020.05.15-arm64.raucb",
            "md5": "4a2ede78e6f59c56f19548886ca6070d",
            "size": 4312084
        }
    ]
}
```

##### Обработка запросов от агентов

Рассмотрим пример обработки запроса `GET /firmware/1.x/target_state?hardware=HW&deviceid=DEVICEID&slots=SLOT`.

1. По значениям `hardware, deviceid` и таблице `device_branch` определяется `branch` прошивки.
2. Идём по таблице `firmware_rollout_history` от самой новой записи к самой старой, отфильтровав её по `firmware_rollout.hardware, firmware_rollout.branch, firmware_rollout.slot`
На каждом шаге проверяем, попадает ли наш `deviceid` в scope (с учетом `firmware_rollout.seed` и `firmware_rollout.perent`) текущей записи о раскатке.
Если не попадает, то переходим к следующей записи.
Если попадает, то возвращаем ответ на основе этой записи о раскатке.
Если мы дошли до конца таблицы, но так и не встретили запись, под которую подпадает deviceid,
то ошибка - HTTP 404.

Ответ на основе записи о раскатке:
- Если запись со status='inactive', то HTTP 204.
- Если запись со status='active', то HTTP 200 и соответствующее записи целевое состояние.

Критерий определения принадлежности устройства к эксперименту:  `hash(deviceid + seed) % 100 < percent`.


### Cli для управления прошивками и раскатками
Cli поддерживает следующие операции:
1. Залить или удалить прошивку.
2. Показать список существующих прошивок (с поддержкой фильтрации).
3. Определить целевое состояние прошивки для окружения, в том числе для случайного подмножества устройств.
4. Добавить устройство в окружение или удалить его из окружения
5. Показать окружение для устройства, показать все устройства для данного окружения

Для авторизации пользователя Cli получает TVM-токен либо через переменную окружения, либо посредством ssh-ключа пользователя, запустившего cli.

#### Заливка новой прошивки
```
$ cli upload  --hardware mrc-nanopi-neo4 --slot rootfs --version 1.0.0-1 path_to_file

{
    "id": "1234",
    "hardware": "mrc-nanopi-neo4",
    "slot": "rootfs",
    "version_seq": 123,
    "version": "1.0.1-1",
    "url": "http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4a2ede78e6f59c56f19548886ca6070d",
    "md5": "4a2ede78e6f59c56f19548886ca6070d",
    "size": 4312084
}
```


1. Выполняет запрос `PUT /v2/firmware/upload/start` в ответ получает идентификатор заливки.
2. Разделяет файл прошивки на фрагменты по `n MB`, для каждого фрагмента выполняет запрос `PUT /v2/firmware/upload/add_part?id=&part=`
3. Выполняет запрос `PUT /v2/firmware/upload/finish?id=&hardware=nanopi-neo4&slot=rootfs&version=`

#### Управление целевым состоянием

##### Создание rollout

Создает раскатку в состоянии `inactive`.
```
$ cli rollout create --hardware mrc-nanopi-neo4 --slot rootfs --branch stable --version VER

{
    id: 100,
    branch: stable,
    percent: 0,
    status: inactive,
    created_by: quoter,
    created_at: 2020-06-02T12:01:00,
    firmware: {
        hardware: mrc-nanopi-neo4,
        slot: rootfs,
        version_seq: 124,
        version: 1.0.1-1
        download_url: http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4a2ede78e6f59c56f19548886ca6070d
        content_md5: 53f31a089339194f333d2e3995dbb05e,
        content_size: 4312084
    }
}
```

##### Выкатка rollout на процент устройст

Активирует раскатку и устанавливает процент для раскатки.
```
$ cli rollout expand --rollout-id ROLLOUT_ID --percent 10

{
    id: 100,
    branch: stable,
    percent: 10,
    status: active,
    created_by: quoter,
    created_at: 2020-06-02T12:01:00,
    firmware: {
        hardware: mrc-nanopi-neo4,
        slot: rootfs,
        version_seq: 124,
        version: 1.0.1-1
        download_url: http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4a2ede78e6f59c56f19548886ca6070d
        content_md5: 53f31a089339194f333d2e3995dbb05e,
        content_size: 4312084
    }
}
```

##### Приостановка rollout

Останавливает раскатку
```
$ cli rollout pause --rollout-id ROLLOUT_ID

{
    id: 100,
    branch: stable,
    percent: 10,
    status: inactive,
    created_by: quoter,
    created_at: 2020-06-02T12:01:00,
    firmware: {
        hardware: mrc-nanopi-neo4,
        slot: rootfs,
        version_seq: 124,
        version: 1.0.1-1
        download_url: http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4a2ede78e6f59c56f19548886ca6070d
        content_md5: 53f31a089339194f333d2e3995dbb05e,
        content_size: 4312084
    }
}
```

##### Возобносление rollout

Активирует раскатку
```
$ cli rollout resume --rollout-id ROLLOUT_ID

{
    id: 100,
    branch: stable,
    percent: 10,
    status: active,
    created_by: quoter,
    created_at: 2020-06-02T12:01:00,
    firmware: {
        hardware: mrc-nanopi-neo4,
        slot: rootfs,
        version_seq: 124,
        version: 1.0.1-1
        download_url: http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4a2ede78e6f59c56f19548886ca6070d
        content_md5: 53f31a089339194f333d2e3995dbb05e,
        content_size: 4312084
    }
}
```

#### Получение информации о текущем целевом состоянии

```
$cli rollout target --hardware mrc-nanopi-neo4 [--slot rootfs] [--branch stable]

[
    {
        branch: stable,
        percent: 100,
        firmware: {
            hardware: mrc-nanopi-neo4,
            slot: rootfs,
            version_seq: 123,
            version: 1.0.0-1
            download_url: http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4ccbe11d031968d5c4297d0eec769b9a
            content_md5: 4ccbe11d031968d5c4297d0eec769b9a,
            content_size: 4312000
        }
    },
    {
        branch: stable,
        percent: 10,
        firmware: {
            hardware: mrc-nanopi-neo4,
            slot: rootfs,
            version_seq: 124,
            version: 1.0.1-1
            download_url: http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4a2ede78e6f59c56f19548886ca6070d
            content_md5: 53f31a089339194f333d2e3995dbb05e,
            content_size: 4312084
        }
    }
]
```

#### Получение информации об истории изменения состояний

```
$cli rollout history --hardware mrc-nanopi-neo4 [--slot rootfs] [--branch stable] [--results 100] [--offset 0]

[
    {
        branch: stable,
        percent: 10,
        status: active,
        created_by: quoter,
        created_at: 2020-06-02T12:01:00,
        firmware: {
            hardware: mrc-nanopi-neo4,
            slot: rootfs,
            version_seq: 124,
            version: 1.0.1-1
            download_url: http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4a2ede78e6f59c56f19548886ca6070d
            content_md5: 53f31a089339194f333d2e3995dbb05e,
            content_size: 4312084
        }
    },
    {
        branch: stable,
        percent: 0,
        status: inactive,
        created_by: quoter,
        created_at: 2020-06-02T12:00:00,
        firmware: {
            hardware: mrc-nanopi-neo4,
            slot: rootfs,
            version_seq: 124,
            version: 1.0.1-1
            download_url: http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4a2ede78e6f59c56f19548886ca6070d
            content_md5: 53f31a089339194f333d2e3995dbb05e,
            content_size: 4312084
        }
    },
    {
        branch: stable,
        percent: 100,
        status: active,
        created_by: quoter,
        created_at: 2020-06-01T12:00:00,
        firmware: {
            hardware: mrc-nanopi-neo4,
            slot: rootfs,
            version_seq: 123,
            version: 1.0.0-1
            download_url: http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4ccbe11d031968d5c4297d0eec769b9a
            content_md5: 4ccbe11d031968d5c4297d0eec769b9a,
            content_size: 4312000
        }
    },
    {
        branch: stable,
        percent: 50,
        status: active,
        created_by: quoter,
        created_at: 2020-05-25T12:00:00,
        firmware: {
            hardware: mrc-nanopi-neo4,
            slot: rootfs,
            version_seq: 123,
            version: 1.0.0-1
            download_url: http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4ccbe11d031968d5c4297d0eec769b9a
            content_md5: 4ccbe11d031968d5c4297d0eec769b9a,
            content_size: 4312000
        }
    },
    {
        branch: stable,
        percent: 10,
        status: active,
        created_by: quoter,
        created_at: 2020-05-15T12:00:00,
        firmware: {
            hardware: mrc-nanopi-neo4,
            slot: rootfs,
            version_seq: 123,
            version: 1.0.0-1
            download_url: http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4ccbe11d031968d5c4297d0eec769b9a
            content_md5: 4ccbe11d031968d5c4297d0eec769b9a,
            content_size: 4312000
        }
    },
    {
        branch: stable,
        percent: 0,
        status: inactive,
        created_by: quoter,
        created_at: 2020-05-14T12:00:00,
        firmware: {
            hardware: mrc-nanopi-neo4,
            slot: rootfs,
            version_seq: 123,
            version: 1.0.0-1
            download_url: http://s3.yandex.net/maps-mrc-drive-package/mrc_nanopi-neo4_rootfs_4ccbe11d031968d5c4297d0eec769b9a
            content_md5: 4ccbe11d031968d5c4297d0eec769b9a,
            content_size: 4312000
        }
    },
    ...
]

```

#### Управление окружением для устройства
##### Добавить устройство в окружение
```
$cli device-branch add --hardware mrc-nanopi-neo4 --device-id 0eb53c63c764 --branch testing

{
    hardware: mrc-nanopi-neo4;
    deviceid: 0eb53c63c764;
    branch: testing;
}
```

##### Удалить устройство из окружения
```
$cli device-branch remove --hardware mrc-nanopi-neo4 --deviceid 0eb53c63c764
```

##### Показать устройства в окружении
```
$cli device-branch list --hardware mrc-nanopi-neo4 [--deviceid 0eb53c63c764] [--branch testing]
{
    {
        hardware: mrc-nanopi-neo4;
        deviceid: 0eb53c63c764;
        branch: testing;
    },
    ...
}

```

### Мобильная часть

Единицей обновления будет являться образ дискового раздела. Для надежного обновления на устройстве
будут выделены дублирующие разделы, в каждый момент один из которых активен, а второй, неактивный,
может использоваться для установки в него обновлений.

#### Обновление с помощью RAUC

Реализация этой схемы будет сделана на основе [RAUC](https://rauc.io/) — решения для обновления встроенных linux-систем,
 которое обеспечивает безопасное обновление с возможностью отката на стабильную версию при неудачном обновлении.
Пара дублирующих разделов будет создана для каждого типа разделов, подлежащих обновлению. Например, на устройстве можно
создать 2 rootfs раздела и 2 appfs раздела, но при этом один персистентный data-раздел, который будет монтироваться
при загрузке любой из двух rootfs. Также в единственном экземпляре должен присутствовать раздел с загрузчиком.
Обновление раздела с загрузчиком также поддерживается RAUC, однако без возможности отката в случае ошибки, поэтому должно
выполняться с большой осторожностью. Для переключения на обновленный раздел необходима интеграция с загрузчиком.
RAUC поддерживает основные загрузчики, используемые для встроенных систем: U-boot, Grub, Barebox.
RAUC оперирует собственным форматом бандлов (файлы с расширением `.raucb`), содержащих внутри образ необходимого
раздела и мета-информацию для его установки. Бандлы создаются на сервере и подписываются с помощью ключа.
На устройство доставляется сертификат для проверки подлинности бандла.

#### Сборка прошивки с помощью YOCTO

Гибким инструментом для создания кастомизированной прошивки с linux под конкретное устройство является
[Yocto](https://www.yoctoproject.org/). В Yocto прошивка собирается как конструктор из блоков, называемых
рецептами (recipes), и конфигурационных файлов. Наборы рецептов и конфигурационных файлов объединяются в
логические группы, называемые слоями (layers). Yocto поставляет набор базовых слоев, содержащих рецепты для с
борки ядра, основных модулей, загрузчика, множества распространенных пакетов и т.д. Рецепты могут расширять друг
друга, так, например, в собственном рецепте можно дополнить базовый рецепт сборки ядря, добавив в него
необходимый патч. Минимально, для кастомизации сборки под целевое железо требуется добавить слой, называемый
board support package (BSP). Для распространенных устройств BSP-слои часто уже написаны и находятся в открытом доступе.
В проекте интеграции Зеркал с Яндекс-Драйвом к стандартным слоям, идущим в составе Yocto, добавляются слои:
 - `meta-rauc` для интеграции с RAUC,
 - `meta-nanopi-neo4` — BSP слой для поддержки платы nanopi,
 - `meta-mrc` — слой с компонентами mrc, отвечающими за бизнес-логику: работу функциональности
    фотосъемки, а также обновления прошивки, диагностику и т.п.

#### Процесс обновления

Перед запуском на устройство должна быть установлена первоначальная прошивка, как минимум содержащая ПО
для собственного обновления. Механизм обновления прошивки будет реализован в systemd-сервисе, который
запускается на старте системы и с определенным интервалом проверяет наличие свежей прошивки на сервере обновлений.
Конфигурация слотов (обновляемых разделов) устройства описывается в конфигурационном файле RAUC, благодаря
чему устройство всегда может узнать текущее состояние разделов и версии, установленные в них. Если целевая
версия прошивки в ответе сервера для данного слота отличается от текущей установленной, обновление будут
скачиваться по ссылке в ответе и устанавливаться средствами RAUC, после чего будет выполнено переключение
на новые раздел и устройство будет перезагружаться. Если загрузка с нового раздела была неуспешной, после
нескольких попыток RAUC переключит загрузку обратно на старый раздел и пометит новый раздел как `bad`.
При очередной проверке обновлений если версия в ответе сервера совпадает с версией, установленной в разделе,
помеченном `bad`, такое обновление будет проигнорировано.

#### Защита от выкатки обновления с фатальной ошибкой

Существует риск, что очередное обновление прошивки со скриптом updater-а будет содержать ошибку, из-за
которой дальнейшие обновления станут невозможны. Для решения этой проблемы на устройствах должна храниться
бэкап-версия updater-a, которая гарантированно работает. В случае завершения updater-скрипта с фатальной
ошибкой текущий updater-скрипт должен подменяться бэкап-версией. При наличии достаточного свободного места
на диске устройства также возможно создать дополнительный rescue-раздел, выполняющие функцию сброса к
первоначальным настройкам. В скрипте загрузчика возможно реализовать логику, по которой при неудачной
загрузке с обоих rootfs-разделов устройство переключится на rescue-раздел. Ту же логику можно реализовать
и в user-space, если в результате самодиагностики выяснилось, что устройство оказалось в неработоспособном
состоянии.

