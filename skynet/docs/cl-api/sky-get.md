# Скачивание данных по идентификатору ресурса (sky get)

Скачивание данных, соответствующих сформированному идентификатору ресурса (результат выполнения команды [sky share](sky-share.md)), на текущий хост.

Также могут быть скачаны ресурсы задачи Sandbox.

{% include [commands-keys-require-copier](_includes/commands-keys/id-commands-keys/require-copier.md) %}

[Формат запуска](sky-get.md#request-format)
[Формат вывода](sky-get.md#response-format)
[Распространенные ошибки (Вики)](https://wiki.yandex-team.ru/skynet/FAQ2/#naiboleeverojatnyeoshibkiichtosnimidelat)

## Формат запуска {#request-format}

```
sky get [опциональные ключи] <идентификатор ресурса>
```

{% cut "Возможные ключи и значения" %}

**Параметры аутентификации**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** || 

|| `-u, --user` | Скачивать ресурсы с правами текущего пользователя и выставлять соответствующие права получаемым файлам и каталогам.

Используется, если ресурсы необходимо скачать в каталог, доступ к которому ограничен. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||
|#

**Параметры вывода**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** || 

|| `--traceback` | Выводить расширенный traceback ошибок. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-p, --progress` | Отображать индикатор выполнения.

>Если ключ указан, возвращается динамическая строка, отражающая:
- ход выполнения команды;
- время, прошедшее с начала выполнения;
- сведения о суммарном количестве объектов, соответствующих заданным критериям;
- количестве обработанных объектов. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| ` --progress-format=<значение>` | Отображать индикатора выполнения в указанном формате.

Возможные значения:

- «human» — динамическая строка. Используется по умолчанию, если ключ не указан.
- «json» — прогресс выполнения в формате `json`. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %}

{% note warning %}

Необходимо использовать с ключом `-p`.

{% endnote %} ||

|| ` --progress-version=<номер версии>` | Использовать указанную версию индикатора выполнения (для индикатора в формате `json`). Обеспечивает обратную совместимость.

Возможное значение на сентябрь 2018 года — «1». Используется по умолчанию, если ключ не указан. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %}

{% note warning %}

Необходимо использовать с ключом ` --progress-format=json`.

{% endnote %} ||

|| `--progress-report-freq=<значение>` | Установить максимальную частоту (в милисекундах), с которой обновляется индикатор выполнения в формате `json`.

Значение по умолчанию — «0». Используется, если ключ не указан. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %}

{% note warning %}

Необходимо использовать с ключом ` --progress-format=json`.

{% endnote %} ||

Параметры запуска и выполнения

|| `--opts=<значение>` | Отладочный параметр. Используется для проведения экспериментов. За дополнительной информацией обратитесь в [группу SkyNet](https://staff.yandex-team.ru/departments/yandex_search_tech_searchinfradev_skynet/). | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-t <значение>`, 
`--timeout=<значение>` | Ограничить время, в течение которого необходимо предпринимать попытки выполнить команду.

Если команда не выполнена на удаленном хосте в течение указанного времени, процедура прерывается и возвращается соответствующая ошибка.

Значение задается в секундах. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-P <приоритет>`, 
`--priority=<приоритет>` | Установить сетевой приоритет задания на скачивание.

Возможные значения:

- «Idle».
- «Low».
- «BelowNormal».
- «Normal» (используется по умолчанию, если ключ не указан).
- «AboveNormal».
- «High».
- «RealTime». | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| ` -N <тип сети>`, 
`--network=<тип сети>` | Использовать при скачивании указанный тип сети.

Возможные значения:

- <q>Backbone</q> — сеть, предназначенная для передачи трафика, генерируемого пользовательскими запросами.
- <q>Fastbone</q> — сеть, предназначенная для передачи технологического трафика.
- <q>Auto</q> — автоматический выбор типа сети.    

{% note warning %}

 Если на сервере присутствует Fastbone, то Copier будет пытаться скачать данные только по этой сети, даже если она недоступна. Если Fastbone отсутствует, скачивание будет выполняться по Backbone.
 
 {% endnote %}
 
 Значение по умолчанию задается в Genisys в [конфигурации сервиса Copier](https://genisys.yandex-team.ru/sections/skynet.services.copier) ().
 
 Подробные сведения об архитектуре Backbone- и Fastbone-сетей приведены в [Вики](http://wiki.yandex-team.ru/PavelKiselev/DC-design). | 
 
 {% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-D <режим дедупликации>`, 
`--deduplicate=<режим дедупликации>` | Применить дедупликацию при скачивании файлов (выполняется проверка на совпадение пользователя и контрольной суммы).

Возможные значения:

- «No» — режим выключен. Используется по умолчанию, если ключ не указан.
- «Hardlink»  — формировать жесткую ссылку.
- «Symlink» — формировать символьную ссылку. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--max-dl-speed=<MAX_DL_SPEED>` | Ограничить скорость скачивания данных по сети. Задается в байтах (например, 10M) или в мегабитах в секунду (например, 10 Mbits) | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--max-ul-speed=<MAX_UL_SPEED>` | Ограничить скорость отдачи данных по сети. Задается в байтах (например, 10M) или в мегабитах в секунду (например, 10 Mbits) | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--tag=<тег>` | Технический параметр. Присвоить тег загрузке. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-d <путь до каталога>`, 
`--dir=<путь до каталога>` | Указать каталог на текущем сервере, в который необходимо скопировать содержимое ресурсов.

Если ключ не указан, ресурсы копируются в текущий каталог. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--sign-key=<ключ>` | Подписать ресурс сгенерированным ранее ECDSA-ключом.

Технический параметр. За дополнительной информацией обратитесь в [группу SkyNet](https://staff.yandex-team.ru/departments/yandex_search_tech_searchinfradev_skynet/). | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||
|#

**Ресурсы**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** || 

|| `идентификатор ресурса` | Идентификатор ресурса, содержимое которого необходимо скачать.

Поддерживаются следующие типы идентификаторов:

- Торрент-идентификатор. Возвращается по умолчанию при выполнении команды [sky-share](sky-share.md).

Формат указания: `rbtorrent:<идентификатор ресурса>`

- Архив (tar, tbz2, tgz), закодированный в Base64. Может быть сформирован при выполнении команды [sky-share](sky-share.md). При скачивании распаковывается в указанный каталог.

Формат указания: `tar:<строка, закодированная в Base64>`, `tbz2:<строка, закодированная в Base64>`, `tgz:<строка, закодированная в Base64>`.

- Ресурсы задачи Sandbox. Скачиваются все ресурсы со статусом «READY».

Формат указания: `sandbox:<идентификатор задачи в Sandbox (task_id)>`, `sandbox-task:<идентификатор задачи в Sandbox (task_id)>`, `sbt:<идентификатор задачи в Sandbox (task_id)>`.

- Ресурсы из Sandbox.

Формат указания: `sandbox-resource:<идентификатор ресурсов в Sandbox (resource_id)>`, `sbr:<идентификатор ресурсов в Sandbox (resource_id)>`.

- Несколько ресурсов.

Формат указания: `all:<тип идентификатора 1>:<идентификатор ресурса 1>,<тип идентификатора 2>:<идентификатор ресурса 2>,...,<тип идентификатора N>:<идентификатор ресурса N>`.

- Один из указанных ресурсов.

Попытки скачать ресурсы выполняются последовательно (по принципу FIFO). Операция прерывается после первого успешного скачивания ресурсов.

Формат указания: `anyall`:`<тип идентификатора 1>:<идентификатор ресурса 1>,<тип идентификатора 2>:<идентификатор ресурса 2>,...,<тип идентификатора N>:<идентификатор ресурса N>`. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||
|#

{% endcut %}

## Формат вывода {#response-format}

В случае успешного выполнения команды возвращается управление командной строкой.

#### Узнайте больше

* [Распространенные ошибки](https://wiki.yandex-team.ru/skynet/FAQ1/#naiboleeverojatnyeoshibkiichtosnimidelat)