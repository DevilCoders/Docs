# Получение содержимого сформированного ресурса (sky files)

Возвращает список файлов и каталогов, которые относятся к указанному идентификатору ресурса (полученном при выполнении команды [sky share](sky-share.md)).
{% note info %}

По умолчанию возвращает список файлов и каталогов в [стандартном](#standard-output) формате (репрезентация словаря Python через функцию ).

{% endnote %}

{% include [commands-keys-require-copier](_includes/commands-keys/id-commands-keys/require-copier.md) %}

[Формат запуска](sky-files.md#request-format)
[Формат вывода](sky-files.md#response-format)
[Распространенные ошибки (Вики)](https://wiki.yandex-team.ru/skynet/FAQ2/#naiboleeverojatnyeoshibkiichtosnimidelat)

## Формат запуска {#request-format}

```
sky files [опциональные ключи] <идентификатор ресурса>
```

{% cut "Возможные ключи и значения" %}



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

|| `-f, --full` | Возвращать сведения о каталогах и символьных ссылках. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--json` | Возвращать ответ в формате `JSON`. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--ls` | Для каждого файла возвращать права доступа, имя владельца, имя группы, размер файла в байтах и timestamp.

Содержимое сортируется по именам файлов. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--lsh` | Для каждого файла возвращать права доступа, имя владельца, имя группы, размер файла (с аббревиатурой единицы измерения количества информации) и timestamp.

Содержимое сортируется по именам файлов. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--lsS` | Для каждого файла возвращать права доступа, имя владельца, имя группы, размер файла (с аббревиатурой единицы измерения количества информации) и timestamp.

Содержимое сортируется по размеру файлов. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

||`--lshS` | Для каждого файла возвращать права доступа, имя владельца, имя группы, размер файла (с аббревиатурой единицы измерения количества информации) и timestamp.

Содержимое сортируется по размеру файлов. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||
|#

**Параметры запуска и выполнения**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** || 

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
 |#

**Ресурсы**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** || 

|| `идентификатор ресурса` | Идентификатор ресурса, содержимое которого необходимо получить.

Идентификатор возвращается в результате выполнения команды [sky-share](sky-share.md). | Обязательный. ||
|#

{% endcut %}

## Формат вывода {#response-format}

{% include [response-format-response-format-depends-on](_includes/sky-list/id-response-format/response-format-depends-on.md) %}


- [Стандартный](#standard-output) (ключи [`--json`](#json-row), [`--ls`](#ls-row), [`--lsh`](#lsh-row), [`--lsS`](#lss-row), [`--lsh`](#lsh-row), [`--lsS`](#lss-row) и [`--lshS`](#lshs-row) не указаны).
- [JSON](#json) (ключ [`--json`](#json-row)).
- [Расширенный (сортировка по именам файлов)](#additional-output) (ключ [`--ls`](#ls-row)).
- [Расширенный с аббревиатурой единицы измерения информации (сортировка по именам файлов)](#additional-info-sortby-filename-acr) (ключ [`--lsh`](#lsh-row)).
- [Расширенный (сортировка по размерам файлов)](#additional-output-sortby-filesize) (ключ [`--lsS`](#lss-row)).
- [Расширенный с аббревиатурой единицы измерения информации (сортировка по размерам файлов)](#additional-info-sortby-filesize-acr) (ключ [`--lshS`](#lshs-row)).

Если указан ключ [`-f`](#full-row), в выводе также присутствует информация о каталогах и символьных ссылках.

### Стандартный {#standard-output}

Возвращается, если не указаны ключи [`--json`](#json-row), [`--ls`](#ls-rown), [`--lsh`](#lsh-row), [`--lsS`](#lss-row), [`--lsh`](#lsh-row), [`--lsS`](#lss-row) и [`--lshS`](#lshs-row).

Содержит множество записей об объектах ресурса. Объекты разделяются запятой и символом пробела.

Является репрезентацией словаря Python через функцию .

Возможные типы объектов:

- Файл.
- Каталог.

Запись для каждого объекта может содержать строковые поля, приведенные в таблице ниже.

#|
|| **Поле** | **Описание** | **Объекты** ||
|| `executable` | Признак, указывающий является ли файл исполняемым.

Возможные значения:
- «True» — файл является исполняемым.
- «False» — файл не является исполняемым. | Файлы ||

|| `md5sum` | MD5-хеш файла. | 

{% include [response-format-files](_includes/sky-files/id-response-format/files.md) %} ||

|| `type` | Тип объекта, которому соответствует запись.

Возможные значения:

- «dir» — каталог.
- «file» — файл. | Файлы и каталоги ||

|| `name` | Название объекта. | 

{% include [response-format-files-and-dirs](_includes/sky-files/id-response-format/files-and-dirs.md) %} ||

|| `size` | Размер объекта. | 

{% include [response-format-files](_includes/sky-files/id-response-format/files.md) %} ||
|#

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky files -f rbtorrent:38b19faab2868fb20b7677030974a08f48ff1d88
> ```
> 
> Ресурс, доступный по идентификатору `rbtorrent:38b19faab2868fb20b7677030974a08f48ff1d88`, содержит каталог `temp`. В каталоге содержатся файлы `test.txt`, `test2` и `test3`.
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> [{'type': 'dir', 'name': 'temp'}, {'executable': False, 'md5sum': 'ad850e1358c90348f7bab5a111bed931', 'type': 'file', 'name': 'temp/test.txt', 'size': 17}, {'executable': False, 'md5sum': '49c722281ed2b30de9f1b20b2f8500e8', 'type': 'file', 'name': 'temp/test2', 'size': 1263}, {'executable': False, 'md5sum': 'ad850e1358c90348f7bab5a111bed931', 'type': 'file', 'name': 'temp/test3', 'size': 17}]
> ```

### JSON {#json}

Содержит множество записей об объектах ресурса. Объекты разделяются запятой и символом пробела.Данные передаются в формате JSON.

{% include [response-format-the-following-object-types](_includes/sky-files/id-response-format/the-following-object-types.md) %}

- Файл.
- Каталог.

{% include [response-format-each-record-contains](_includes/sky-files/id-response-format/each-record-contains.md) %}

#|
|| **Поле** | **Описание** | **Объекты** ||
|| `executable` | Признак, указывающий является ли файл исполняемым.

Возможные значения:
- «True» — файл является исполняемым.
- «False» — файл не является исполняемым. | Файлы ||

|| `md5sum` | MD5-хеш файла. | 

{% include [response-format-files](_includes/sky-files/id-response-format/files.md) %} ||

|| `type` | Тип объекта, которому соответствует запись.

Возможные значения:

- «dir» — каталог.
- «file» — файл. | Файлы и каталоги ||

|| `name` | Название объекта. | 

{% include [response-format-files-and-dirs](_includes/sky-files/id-response-format/files-and-dirs.md) %} ||

|| `size` | Размер объекта. | 

{% include [response-format-files](_includes/sky-files/id-response-format/files.md) %} ||
|#


> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky files -f --json rbtorrent:38b19faab2868fb20b7677030974a08f48ff1d88
> ```
> 
> {% include [response-format-example-description](_includes/sky-files/id-response-format/example-description.md) %}
> 
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> [{"type": "dir", "name": "temp"}, {"executable": false, "md5sum": "ad850e1358c90348f7bab5a111bed931", "type": "file", "name": "temp/test.txt", "size": 17}, {"executable": false, "md5sum": "49c722281ed2b30de9f1b20b2f8500e8", "type": "file", "name": "temp/test2", "size": 1263}, {"executable": false, "md5sum": "ad850e1358c90348f7bab5a111bed931", "type": "file", "name": "temp/test3", "size": 17}]
> ```

### Расширенный (сортировка по именам файлов) {#additional-output}

Запись о каждом объекте ресурса приводится с новой строки и содержит следующие сведения:

- Права доступа.
- Владелец объекта.
- Группа, к которой относится владелец объекта.
- Размер файла в байтах.
- Название объекта.

Объекты сортируются в алфавитном порядке.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky files -f --ls rbtorrent:38b19faab2868fb20b7677030974a08f48ff1d88
> ```
> 
> {% include [response-format-example-description](_includes/sky-files/id-response-format/example-description.md) %}
> 
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> Resource 'rbtorrent:38b19faab2868fb20b7677030974a08f48ff1d88' (total items 4, size 1297):
> drwx skynet skynet           0 --- -- --:-- temp
> -rw- skynet skynet          17 --- -- --:-- temp/test.txt
> -rw- skynet skynet        1263 --- -- --:-- temp/test2
> -rw- skynet skynet          17 --- -- --:-- temp/test3
> ```

### Расширенный с аббревиатурой единицы измерения информации (сортировка по именам файлов) {#additional-info-sortby-filename-acr}

{% include [response-format-each-record-from-new-line](_includes/sky-files/id-response-format/each-record-from-new-line.md) %}


- Права доступа.
- Владелец объекта.
- Группа, к которой относится владелец объекта.
- Размер файла. Если размер превышает 999 байт, содержит аббревиатуру, определяющую единицу измерения количества информации (например, <q>K</q> для килобайт).
- Название объекта.

{% include [response-format-alphabetical-order](_includes/sky-files/id-response-format/alphabetical-order.md) %}


> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky files -f --lsh rbtorrent:38b19faab2868fb20b7677030974a08f48ff1d88
> ```
> 
> {% include [response-format-example-description](_includes/sky-files/id-response-format/example-description.md) %}
> 
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> Resource 'rbtorrent:38b19faab2868fb20b7677030974a08f48ff1d88' (total items 4, size 1.27K):
> drwx skynet skynet        0 --- -- --:-- temp
> -rw- skynet skynet       17 --- -- --:-- temp/test.txt
> -rw- skynet skynet    1.23K --- -- --:-- temp/test2
> -rw- skynet skynet       17 --- -- --:-- temp/test3
> ```

### Расширенный (сортировка по размерам файлов) {#additional-output-sortby-filesize}

{% include [response-format-each-record-from-new-line](_includes/sky-files/id-response-format/each-record-from-new-line.md) %}


- Права доступа.
- Владелец объекта.
- Группа, к которой относится владелец объекта.
- Размер файла в байтах.
- Название объекта.

Объекты сортируются в порядке возрастания размера объектов.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky files -f --lsS rbtorrent:38b19faab2868fb20b7677030974a08f48ff1d88
> ```
> 
> {% include [response-format-example-description](_includes/sky-files/id-response-format/example-description.md) %}
> 
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> Resource 'rbtorrent:38b19faab2868fb20b7677030974a08f48ff1d88' (total items 4, size 1297):
> drwx skynet skynet           0 --- -- --:-- temp
> -rw- skynet skynet          17 --- -- --:-- temp/test.txt
> -rw- skynet skynet          17 --- -- --:-- temp/test3
> -rw- skynet skynet        1263 --- -- --:-- temp/test2
> ```

### Расширенный с аббревиатурой единицы измерения информации (сортировка по размерам файлов) {#additional-info-sortby-filesize-acr}

{% include [response-format-each-record-from-new-line](_includes/sky-files/id-response-format/each-record-from-new-line.md) %}


- Права доступа.
- Владелец объекта.
- Группа, к которой относится владелец объекта.
- Размер файла. Если размер превышает 999 байт, содержит аббревиатуру, определяющую единицу измерения количества информации (например, <q>K</q> для килобайт).
- Название объекта.

{% include [response-format-order-by-file-size](_includes/sky-files/id-response-format/order-by-file-size.md) %}


> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky files -f --lshS rbtorrent:38b19faab2868fb20b7677030974a08f48ff1d88
> ```
> 
> {% include [response-format-example-description](_includes/sky-files/id-response-format/example-description.md) %}
> 
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> drwx skynet skynet        0 --- -- --:-- temp
> -rw- skynet skynet       17 --- -- --:-- temp/test.txt
> -rw- skynet skynet       17 --- -- --:-- temp/test3
> -rw- skynet skynet    1.23K --- -- --:-- temp/test2
> ```

#### Узнайте больше

* [Распространенные ошибки](https://wiki.yandex-team.ru/skynet/FAQ1/#naiboleeverojatnyeoshibkiichtosnimidelat)