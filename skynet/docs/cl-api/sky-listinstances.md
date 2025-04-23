# Доступные инстансы (sky listinstances)

Возвращает список инстансов для группы [GenCfg](https://wiki.yandex-team.ru/jandekspoisk/sepe/gencfg) (`G@`) или сервиса в [Nanny](https://wiki.yandex-team.ru/runtime-cloud/nanny/) (`f@`).

[Формат запуска](sky-listinstances.md#request-format)
[Формат вывода](sky-listinstances.md#response-format)
[Распространенные ошибки (Вики)](https://wiki.yandex-team.ru/skynet/FAQ2/#naiboleeverojatnyeoshibkiichtosnimidelat)

## Формат запуска {#request-format}

```
sky listinstances [опциональные ключи] <группирующие объекты>
```
{% cut "Возможные ключи и значения" %}

**Параметры запуска и выполнения**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** ||

|| ` --dont_check_hosts ` | Не выполнять проверку хостов в DNS.

Ускоряет выполнение команды, но при этом ответственность за проверку доступности хостов ложится на пользователя. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %}

Хосты, на которых выполняется команда, должны быть заданы списком. ||
|#

**Параметры вывода**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** ||

|| `--cut-domain` | Возвращать сокращенные названия хостов.

Например, если при выполнении команды найдены хосты `ws18-211.yandex.ru`, `ws18-212.yandex.ru`, `ws18-213.yandex.ru` и `ws18-214`, результат принимает следующий вид:
```
ws18-211
ws18-212
ws18-213
ws18-214
```
{% note info %}

Названия хостов определяются правилами в [Genisys](https://genisys.yandex-team.ru/).
(**skynet**  → **tools** → **sky** → **<название правила>** → **set of domain**). 

{% endnote %} | {% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %}

{% note info "Ограничение" %} 

Обеспечивает обратную совместимость при замене вызовов утилиты `yr` с ключом `LIST` в различных скриптах.

Использование ключа для других целей категорически запрещено.

{% endnote %} ||

|| `-f <формат>, --format=<формат>` | Выводить результат выполнения команды в указанном формате.

Возможные значения:
- ls — построчный. Используется по умолчанию, если ключ не указан;
- json — JSON;
- msgpack — MessagePack. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--no-tag` | Возвращать только список инстансов без идентификатора тега, к которому они относятся. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||
|#

**Хосты и/или группирующие объекты, на которых должна выполняться команда**

{% note alert %}

Требуемые хосты и/или группы должны быть указаны только одним из доступных способов.

{% endnote %}

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** ||

|| `группирующие объекты` | Список хостов и/или группирующих объектов, на хостах которых необходимо выполнять команду.

[Формат указания](targets-classif.md#syntax) зависит от используемого синтаксиса. Если указан ключ `-N`, значения необходимо указывать в соответствии с [калькулятором Блинова](https://doc.yandex-team.ru/generated/skynet/sky/blinovcalc.html).

Если при использовании калькулятора Блинова не указан [префикс](https://doc.yandex-team.ru/generated/skynet/sky/blinovcalc.html?iframed=true#id3), считается, что указаны хосты. Например, конструкции «s33-237» и «h@s33-237» являются взаимозаменяемыми. | 

{% note alert %}

Не должен использоваться с ключом `--hosts`. В остальных случаях является обязательным.

{% endnote %} ||

|| `--hosts=<путь до файла>` | Выполнять команду на хостах, указанных в файле. Расширение файла не регламентировано.

Формат указания хостов в файле:
```
<хост 1>
<хост 2>
...
<хост N>
```

Каждый хост указывается с новой строки. Допустимо указание расширенного или сокращенного названия. Например, для выполнения команды на хостах `ws6-100` и `ws6-101` файл должен содержать следующие записи:
```
ws6-100
ws6-101
``` 
| {% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %}

{% note alert %}

Не должен использоваться с ключом `-N`.

{% endnote %} ||
|#

**Устаревшие. Обеспечивают обратную совместимость.**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** ||

|| `-l, --long_names` | Возвращать расширенные названия хостов.

Если ключ указан, каждая строка вывода содержит расширенное название хоста. Например: `ws3-538.yandex.ru`. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|#

{% endcut %}

## Формат вывода {#response-format}

Формат вывода зависит от списка используемых ключей:

- [Построчный](#new-line) (ключ [`-f`](#format-row) со значением <q>ls</q>).
- [JSON](#json) (ключ [`-f`](#format-row) со значением <q>json</q>).
- [MessagePack](#messagepack) (ключ [`-f`](#format-row) со значением <q>msgpack</q>).

### Построчный {#new-line}

Возвращается, если не указаны ключи, определяющие параметры вывода или указан ключ [`-f`](#format-row) со значением <q>ls</q>.

Формат вывода:

```
<слот 1(полное имя хоста:порт)>@<тег>
<слот 2(полное имя хоста:порт)>@<тег>
...
<слот N(полное имя хоста:порт)>@<тег>
```

Результаты разделены символом переноса строки.

> Рассмотрим следующую команду:
> 
> ```
> sky listinstances G@SAS_SKYNET_EXPERIMENT_PORTO
> ```
> 
> Результат выполнения:
> 
> ```
> sas1-1354.search.yandex.net:28636@trunk
> sas1-1712.search.yandex.net:28636@trunk
> sas1-1732.search.yandex.net:28636@trunk
> sas1-1865.search.yandex.net:28636@trunk
> sas1-4205.search.yandex.net:28636@trunk
> sas1-7665.search.yandex.net:28636@trunk
> 
> ```

> Рассмотрим следующую команду:
> 
> ```
> sky listinstances --no_tag G@SAS_SKYNET_EXPERIMENT_PORTO
> ```
> 
> Результат выполнения:
> 
> ```
> sas1-1354.search.yandex.net:28636
> sas1-1712.search.yandex.net:28636
> sas1-1732.search.yandex.net:28636
> sas1-1865.search.yandex.net:28636
> sas1-4205.search.yandex.net:28636
> sas1-7665.search.yandex.net:28636
> 
> ```

### JSON {#json}

Возвращается, если указан ключ [`-f`](#format-row)со значением <q>json</q>.

{% include [response-format-answer-format-par](_includes/sky-listinstances/id-response-format/answer-format-par.md) %}


```
["полное имя инстанса 1", "полное имя инстанса 2", ..., "полное имя инстанса N"]
```

> {% include [response-format-the-following-command](_includes/sky-listinstances/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky listinstances -f json G@SAS_SKYNET_EXPERIMENT_PORTO
> ```
> 
> {% include [response-format-the-following-answer](_includes/sky-listinstances/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> ["sas1-1354.search.yandex.net:28636@trunk", "sas1-1712.search.yandex.net:28636@trunk", "sas1-1732.search.yandex.net:28636@trunk", "sas1-1865.search.yandex.net:28636@trunk", "sas1-4205.search.yandex.net:28636@trunk", "sas1-7665.search.yandex.net:28636@trunk"]
> ```

### MessagePack {#messagepack}

Возвращается, если указан ключ [`-f`](#format-row) со значением <q>msgpack</q>.

В результате выполнения команды возвращается ответ в бинарном формате обмена данными MessagePack.

> Например:
> 
> ```
> sky listinstances -f msgpack G@SAS_SKYNET_EXPERIMENT_PORTO
> ```

#### Узнайте больше

* [Распространенные ошибки](https://wiki.yandex-team.ru/skynet/FAQ1/#naiboleeverojatnyeoshibkiichtosnimidelat)