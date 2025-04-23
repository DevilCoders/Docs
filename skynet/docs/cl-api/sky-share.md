# Формирование идентификатора ресурса (sky share)

Формирует идентификатор ресурсов, хранящихся на текущем сервере. Полученное значение используется для последующего копирования содержимого ресурса.

{% include [commands-keys-require-copier](_includes/commands-keys/id-commands-keys/require-copier.md) %}

[Формат запуска](sky-share.md#request-format)
[Формат вывода](sky-share.md#response-format)
[Распространенные ошибки (Вики)](https://wiki.yandex-team.ru/skynet/FAQ2/#naiboleeverojatnyeoshibkiichtosnimidelat)

## Формат запуска {#request-format}

```
sky share [опциональные ключи] <путь до ресурсов> 
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
|#

**Параметры запуска и выполнения**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** || 

|| `-T <тип идентификатора>`, 
`--transport=<тип идентификатора>` | Задать тип формируемого идентификатора.

Возможные значения:
- «rbtorrent» — торрент-идентификатор. Используется по умолчанию (если ключ не указан);
- «tgz» («tar», «tbz2»>) — архив из файлов на указанном хосте. При копировании (команда [sky-get](sky-get.md)) архив распаковывается на указанных хостах. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-d <путь до каталога>`, 
`--dir=<путь до каталога>` | Перейти к каталогу, относительно которого указывается путь к содержимому формируемого ресурса.

Если ключ не указан, путь определяется относительно текущего каталога.

Например, если команда выполняется в каталоге `home/musiclover`, а доступ необходимо предоставить к файлу  ``home/musiclover/temp/test.txt`` следует выполнить следующую команду:
```sky share -d temp test.txt ```

Если необходимо предоставить доступ к каталогу и содержащимся в нем файлам, следует выполнить следующую команду:
```sky share temp ``` | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-a, --archive` | Копировать символьные ссылки в неизменном виде.

Если ключ не указан, символьные ссылки разворачиваются. В данном случае при [скачивании](sky-get.md) полученного ресурса цель символьной ссылки будет скопирована в соответствующий каталог. Если целью ссылки является несуществующий файл, выполнение команды завершится с ошибкой. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--sign` | Сгенерировать ECDSA-ключ и подписать им ресурс для копирования.

Технический параметр. За дополнительной информацией обратитесь в [группу SkyNet](https://staff.yandex-team.ru/departments/yandex_search_tech_searchinfradev_skynet/). | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--sign-key=<ключ>` | Подписать ресурс сгенерированным ранее ECDSA-ключом.

Технический параметр. За дополнительной информацией обратитесь в [группу SkyNet](https://staff.yandex-team.ru/departments/yandex_search_tech_searchinfradev_skynet/). | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--opts=<значение>` | Отладочный параметр. Используется для проведения экспериментов. За дополнительной информацией обратитесь в [группу SkyNet](https://staff.yandex-team.ru/departments/yandex_search_tech_searchinfradev_skynet/). | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `путь до ресурсов` | Указать путь до ресурсов, к которым необходимо предоставить доступ.

При использовании ключа `-d` указывается путь относительно переданного с ключом. В противном случае указывается путь относительно каталога, в котором выполняется команда. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||
|#

Во время выполнения команды формируется список файлов, создаются хеш-суммы, фиксируется расположение файлов. Полученная информация отправляется на центральный трекер.

{% endcut %}

## Формат вывода {#response-format}

В качестве ответа возвращается идентификатор ресурса для скачивания (`resource id`) в формате:

```
<тип транспорта>:<>
```

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky share temp
> ```
> 
> Так как ключи не указаны, в результате выполнения команды формируется идентификатор (resource id). По идентификатору доступен каталог `temp`, а также все файлы и вложенные каталоги, которые к нему относятся.
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> rbtorrent:2ff1bc82863d2c9bcb6cfb0359d8ff41edd16c4c
> ```

#### Узнайте больше

* [Распространенные ошибки](https://wiki.yandex-team.ru/skynet/FAQ1/#naiboleeverojatnyeoshibkiichtosnimidelat)