# Копирование и запуск бинарного файла с текущего хоста на удаленные (sky launch)

Копирование бинарного файла с текущего хоста на удаленные с последующим запуском.

{% include [commands-keys-require-cqudp-copier](_includes/commands-keys/id-commands-keys/require-cqudp-copier.md) %}

[Формат запуска](sky-launch.md#request-format)
[Формат вывода](sky-launch.md#response-format)
[Распространенные ошибки (Вики)](https://wiki.yandex-team.ru/skynet/FAQ2/#naiboleeverojatnyeoshibkiichtosnimidelat)

## Формат запуска {#request-format}

```
sky launch [опциональные ключи] [каталог на удаленных хостах] [бинарный файл {параметры}]
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

|| `--no_wait` | Игнорировать сигналы потери связи при выполнении команды с (аналог утилиты `nohup`). Используется, если при выполнении команды не важен вывод. | 

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

**Правила копирования и запуска**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** ||

|| `каталог на удаленных хостах` | Путь до каталога на удаленных хостах в котором необходимо запустить бинарный файл. | Обязательный. ||
|| `бинарный файл` | Бинарный файл, который необходимо запустить. Путь указывается относительно текущего каталога. | Обязательный. ||
|| `параметры` | Параметры для запуска бинарного файла. | Необязательный. ||
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

{% endcut %}

## Формат вывода {#response-format}

Возвращается результат и статус выполнения команды на каждом хосте.

После выполнения команды, бинарный файл автоматически удаляется с хостов.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky launch /hol/search/database dbg_meta -p 11211
> ```
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> ================================================================================
> Success on host: localhost
> --------------------------------------------------------------------------------
> Return code: 0
> --------------------------------------------------------------------------------
> TEST
> ================================================================================
> ```

#### Узнайте больше

* [Распространенные ошибки](https://wiki.yandex-team.ru/skynet/FAQ1/#naiboleeverojatnyeoshibkiichtosnimidelat)