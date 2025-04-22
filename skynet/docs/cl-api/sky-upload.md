# Копирование ресурсов текущего сервера на удаленные (sky upload)

Копирование ресурсов текущего хоста на удаленные.

Идентична последовательному выполнению следующих команд:

- [](sky-share.md) на текущем хосте, в результате выполнения которой формируется идентификатор ресурса;
- [](sky-run.md) на удаленных хостах. В качестве команды передается строка .

{% include [commands-keys-require-cqudp](_includes/commands-keys/id-commands-keys/require-cqudp.md) %}

[Формат запуска](sky-upload.md#request-format)
[Формат вывода](sky-upload.md#response-format)
[Распространенные ошибки (Вики)](https://wiki.yandex-team.ru/skynet/FAQ2/#naiboleeverojatnyeoshibkiichtosnimidelat)

## Формат запуска {#request-format}

```
sky upload [опциональные ключи] <путь до ресурсов> <каталог на удаленных серверах> <хосты и/или группирующие объекты>
```

{% cut "Возможные ключи и значения" %}

**Параметры аутентификации** 

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** || 

|| `-u <имя пользователя>`, 
`--user=<имя пользователя>` | Выполнять команду от имени указанного пользователя.

Cм. раздел [Аутентификация](https://doc.yandex-team.ru/Search/skynet-desc/concepts/authentication.html) документа [Skynet. Общее описание](https://doc.yandex-team.ru/Search/skynet-desc/) | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-U` | Выполнять команду от имени текущего пользователя.

{% include [commands-keys-see-user-authentication](_includes/commands-keys/id-commands-keys/see-user-authentication.md) %} | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-A` | Эмулировать ssh-agent при выполнении команды.
Аналог команды , выполняемой с ключом `-A`.

Cм. раздел [Аутентификация](https://doc.yandex-team.ru/Search/skynet-desc/concepts/authentication.html) документа [Skynet. Общее описание](https://doc.yandex-team.ru/Search/skynet-desc/). | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %}

{% note alert %}

Должен использоваться с ключом `-u` или `-U`.

{% endnote %} ||

|| `-i <путь до файла>` | Использовать пользовательский ключ, доступный в указанном файле.
Аналог команды , выполняемой с ключом `-i`. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||
|#

**Параметры запуска и выполнения**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** || 

|| `-s <максимальный интервал>`, 
`--smooth=<максимальный интервал>` | Выполнять команду с задержкой.

Для каждого хоста задержка определяется индивидуально как случайная величина, находящаяся в диапазоне от 0 до максимального интервала (в секундах). | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-t <значение>, --timeout=<значение>` | Ограничить время выполнения команды.

Если команда не выполнена в течение указанного времени, процедура прерывается и возвращается соответствующая ошибка.
Значение задается в секундах. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--step=<количество хостов>` | Запускать команду на указанном количестве хостов одновременно.  После завершения работы на указанном количестве хостов команда выполняется на следующей группе.

Результат возвращается после каждого шага.

Если ключ не задан или указано значение «0» (`--step=0`), команда запускается на всех хостах одновременно.

Применяется для снижения нагрузки на сеть. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--stop-on-error` | Останавливать выполнение команды, если шаг завершился с ошибкой. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %}

{% note alert %}

Должен использоваться с ключом `--step=<количество хостов>`.

{% endnote %} ||

|| `--retry=<количество попыток>` | Задать количество повторных запусков команды на хостах, где она завершилась с ошибкой.

Результат выполнения команды выводится после каждой попытки. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--log_failed_hosts=<путь до файла>` | Записывать в указанный файл имена хостов, на которых команда завершилось с ошибкой.

В дальнейшем этот файл можно указать в значении ключа `--hosts`. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| ` --dont_check_hosts ` | Не выполнять проверку хостов в DNS.

Ускоряет выполнение команды, но при этом ответственность за проверку доступности хостов ложится на пользователя. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} 

Хосты, на которых выполняется команда, должны быть заданы списком. ||

|| `--opts=<значение>` | Отладочный параметр. Используется для проведения экспериментов. За дополнительной информацией обратитесь в [группу SkyNet](https://staff.yandex-team.ru/departments/yandex_search_tech_searchinfradev_skynet/). | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| ` -N <тип сети>, --network=<тип сети>` | Использовать при скачивании указанный тип сети.

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

|| `-d <путь до каталога>, --dir=<путь до каталога>` | Указать каталог на текущем сервере, в который необходимо скопировать содержимое ресурсов.

Если ключ не указан, ресурсы копируются в текущий каталог. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

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

{% endnote %} | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %}

{% note info "Ограничение" %} 

Обеспечивает обратную совместимость при замене вызовов утилиты `yr` с ключом `LIST` в различных скриптах.
Использование ключа для других целей категорически запрещено.

{% endnote %} ||

|| `-v, --verbose` | Увеличить уровень вывода служебной информации в результате выполнения команды.

Требуемый уровень можно регулировать с помощью повтора ключа в команде.

Например, один ключ `-v` инициирует вывод первого уровня служебной информации, по ключу `-vvv` вернется служебная информация первого, второго и третьего уровня. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-q, --quiet` | Уменьшить уровень вывода служебной информации в результате выполнения команды.

Требуемый уровень можно регулировать с помощью повтора ключа в команде.

Например, один ключ `-q` уменьшает количество вывода служебной информации на один уровень, ключ `-qq` — на два уровня. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-p, --progress` | Отображать индикатор выполнения.

Если ключ указан, возвращается динамическая строка, отражающая:
- ход выполнения команды;
- время, прошедшее с начала выполнения;
- сведения о суммарном количестве объектов, соответствующих заданным критериям;
- количестве обработанных объектов. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--traceback` | Выводить расширенный traceback ошибок. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||
|#

**Хосты и/или группирующие объекты, на которых должна выполняться команда**

{% note alert %}

Требуемые хосты и/или группы должны быть указаны только одним из доступных способов.

{% endnote %}

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** || 

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

**Правила копирования**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** || 

|| `путь до ресурсов` | Указать путь до ресурсов, к которым необходимо предоставить доступ. 

При использовании ключа `-d` указывается путь относительно переданного с ключом. В противном случае указывается путь относительно каталога, в котором выполняется команда. |

Обязательный. ||

|| `каталог на удаленных серверах` | Каталог на удаленных хостах, в который необходимо скопировать файлы с текущего. | Обязательный. ||
|#

**Устаревшие. Обеспечивают обратную совместимость.**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** || 

|| `-l, --long_names` | Возвращать расширенные названия хостов.
Если ключ указан, каждая строка вывода содержит расширенное название хоста. Например: `ws3-538.yandex.ru`. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-N, --new_syntax` | Принудительно использовать [калькулятор Блинова](https://doc.yandex-team.ru/generated/skynet/sky/blinovcalc.html).
Если ключ не указан, [формат указания](targets-classif.md#syntax) определяется автоматически. | Необязательный.
{% note alert %}

Не должен использоваться с ключом `--hosts`.

{% endnote %}

||

|| `--old_syntax ` | Принудительно использовать [Устаревший синтаксис](targets-classif.md#old-syntax).

{% include [commands-keys-syntax-key-not-used](_includes/commands-keys/id-commands-keys/syntax-key-not-used.md) %} | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %}

{% include [commands-keys-new-syntax-restriction](_includes/commands-keys/id-commands-keys/new-syntax-restriction.md) %} ||

|| `--cqudp` | Использовать транспорт cqudp. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--cqueue_implementation=<тип транспорта>` | Использовать указанный тип транспорта. Единственное поддерживаемое значение ['cqudp'] | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||
|#

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky upload /etc/hosts /var/tmp G@DEV_TESTING
> ```
> 
> Команда последовательно выполняет следующие действия:
> 
> 1. Формирует идентификатор ресурса для каталога `/etc/hosts` на текущем сервере.
> 1. Копирует ресурсы (соответствующие созданному идентификатору) в каталог `/var/tmp` каждого хоста группы `DEV_TESTING`.

{% endcut %}

## Формат вывода {#response-format}

{% include [response-format-response-format-depends-on](_includes/sky-list/id-response-format/response-format-depends-on.md) %}


- [Без вывода](#no-output) (ключ [`-v`](#verbose-row) отсутствуют).
- [Список хостов с результатами выполнения](#list-with-succes-res) (ключ [`-v`](#verbose-row)).

### Без вывода {#no-output}

Возвращается, если не указан ключ [`-v`](#verbose-row).

В случае успешного завершения возвращается управление командной строкой. При возникновении ошибок возвращается информация о тех хостах, при попытке обратиться к которым проявились ошибки.

### Список хостов с результатами выполнения {#list-with-succes-res}

Возвращается, если указан ключ [`-v`](#verbose-row).

В случае успешного завершения возвращается список хостов, для которых команда успешно выполнена. При проявлении ошибок по крайней мере на одном из хостов возвращается информация об ошибке.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky upload -lv temp db/vartmp/musiclover-temp h@sas1-1037.search.yandex.net h@sas1-1040.search.yandex.net
> ```
> 
> Команда позволяет скопировать содержимое каталога `temp` (относительно текущего пути) в каталог `db/vartmp/musiclover-temp` на хостах `sas1-1037.search.yandex.net` и `sas1-1040.search.yandex.net`. При необходимости соответствующий каталог создается на удаленном хосте.
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> ================================================================================
> Upload successful on 2 host(s): sas1-{1037,1040}.search.yandex.net
> ================================================================================
> ```

#### Узнайте больше

* [Распространенные ошибки](https://wiki.yandex-team.ru/skynet/FAQ1/#naiboleeverojatnyeoshibkiichtosnimidelat)