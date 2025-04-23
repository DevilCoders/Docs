# Выполнение команды (sky run)

Выполнение произвольной команды на удаленных хостах, инстансах или шардах.

Для успешного выполнения команды от имени текущего пользователя необходимо, чтобы удаленный хост содержал пользовательские ключи (см. раздел [Аутентификация](https://doc.yandex-team.ru/Search/skynet-desc/concepts/authentication.html) документа [Skynet. Общее описание](https://doc.yandex-team.ru/Search/skynet-desc/)).

На хосте, с которого запускается , должен быть установлен сервис Сqudp.

[Формат запуска](sky-run.md#request-format)
[Формат вывода](sky-run.md#response-format)
[Запрет на выполнение деструктивных команд](sky-run.md#destructive)
[Распространенные ошибки (Вики)](https://wiki.yandex-team.ru/skynet/FAQ2/#naiboleeverojatnyeoshibkiichtosnimidelat)

## Формат запуска {#request-format}

```
sky run [опциональные ключи] 'команда' <хосты, инстансы, шарды и/или группирующие объекты>
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

|| `--show-cmd` | Отображать выполняемую команду (после преобразований), если она завершилась с ошибкой. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--small-port-range` | Запускать команду на ограниченном числе портов. Список портов задается в конфигурации сервиса cqudp. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| ` --dont_check_hosts ` | Не выполнять проверку хостов в DNS.

Ускоряет выполнение команды, но при этом ответственность за проверку доступности хостов ложится на пользователя. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} 

Хосты, на которых выполняется команда, должны быть заданы списком. ||
|#

**Команда к выполнению**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** || 

|| `-F <путь до файла>, --file=<путь до файла>` | Выполнять команду, указанную в текстовом файле. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %}

{% note alert %}

Не должен использоваться при явном указании команды. В противном случае является обязательным.

{% endnote %} ||

|| `'команда'` | Команда, которую необходимо запустить на удаленном сервере.

Например, для вывода информации о моделях процессоров, используемых на указанных хостах, необходимо ввести следующее значение:
```'sysctl hw.model' ``` | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %}

{% note alert %}

Не должен использоваться с ключом `-F`. В противном случае является обязательным.

{% endnote %} ||
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

|| `--stream` | Выводить результаты в потоковом режиме.

Если ключ указан, результаты от каждого объекта (хоста, инстанса или шарда) выводятся непосредственно после получения ответа. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %}

{% note alert %}

Не должен использоваться с ключом `-p`.

{% endnote %} ||

||`--separate` | Разгруппировать объекты (хосты, инстансы или шарды) в выводе.

Если ключ указан, информация о каждом объекте возвращается с новой строки. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--data-limit=<максимальный размер данных>` | Ограничивать размер возвращаемого сервером ответа.

В значении ключа указывается максимально допустимое значение в мегабайтах. Если ключ не задан, действует ограничение в один мегабайт. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

||`--sort=<тип сортировки>` | Сортировать результаты выполнения команды. Возможные значения:
- «text» — текстовая сортировка.
- «number» — числовая сортировка. | ||
|#

**Хосты и/или группирующие объекты, на которых должна выполняться команда**

{% note alert %}

Требуемые хосты и/или группы должны быть указаны только одним из доступных способов.

{% endnote %}

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** || 

|| `хосты, инстансы, шарды и/или группирующие объекты` | Список хостов и/или группирующих объектов, на хостах которых необходимо выполнять команду.
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

{% include [response-format-response-format-depends-on](_includes/sky-list/id-response-format/response-format-depends-on.md) %}

- [Компактный](#compact-mode-response) (ключи [`--separate`](#separate-row) и [`--stream`](#stream-row) отсутствуют).
- [Без группировки](#separate-mode-response) (ключ [`--separate`](#separate-row)).
- [Потоковый](#stream-response-format) (ключ [`--stream`](#stream-row)).

### Компактный {#compact-mode-response}

Возвращается, если отсутствует ключи [`--separate`](#separate-row) и [`--stream`](#stream-row).

Объекты (хосты, инстансы или шарды), для которых результаты выполнения команды совпадают, группируются.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky run -F temp/command-to-execute h@ws33-192 h@ws33-108 h@ws38-659
> ```
> 
> Команда, которую необходимо выполнить на хостах `ws33-192`, `ws33-108` и `ws33-659` указана в файле `temp/command-to-execute` (путь относительно каталога, из которого вызывается команда `sky run`).
> 
> Содержимое файла `command-to-execute`:
> 
> ```
> sysctl hw.model
> ```
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> ================================================================================
> Success on 1 host(s): +ws38-659
> --------------------------------------------------------------------------------
> hw.model: Intel(R) Xeon(R) CPU E5-2660 0 @ 2.20GHz
> ================================================================================
> 
> ================================================================================
> Success on 2 host(s): +ws33-{108,192}.yandex.ru
> --------------------------------------------------------------------------------
> hw.model: Intel(R) Xeon(R) CPU           E5645  @ 2.40GHz
> ================================================================================
> ```

### Без группировки {#separate-mode-response}

Возвращается, если указан ключ [`--separate`](#separate-row).

Результат для каждого от объекта (хоста, инстанса или шарда) выводится отдельным блоком.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky run -l --separate 'sysctl hw.model' h@ws33-192 h@ws33-108 h@ws38-659
> ```
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> ================================================================================
> Success on host: ws38-659.yandex.ru
> --------------------------------------------------------------------------------
> hw.model: Intel(R) Xeon(R) CPU E5-2660 0 @ 2.20GHz
> 
> ================================================================================
> 
> ================================================================================
> Success on host: ws33-192.yandex.ru
> --------------------------------------------------------------------------------
> hw.model: Intel(R) Xeon(R) CPU           E5645  @ 2.40GHz
> 
> ================================================================================
> 
> ================================================================================
> Success on host: ws33-108.yandex.ru
> --------------------------------------------------------------------------------
> hw.model: Intel(R) Xeon(R) CPU           E5645  @ 2.40GHz
> 
> ================================================================================
> ```

### Потоковый {#stream-response-format}

Возвращается, если указан ключ [`--stream`](#stream-row).

Возвращает ответы от объектов (хостов, инстансов или шардов) по мере получения. Результаты разделены символом переноса строки.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky run --stream 'sysctl hw.model' h@ws33-192 h@ws33-108 h@ws38-659
> ```
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> <ws38-659> hw.model: Intel(R) Xeon(R) CPU E5-2660 0 @ 2.20GHz
> <ws33-108> hw.model: Intel(R) Xeon(R) CPU           E5645  @ 2.40GHz
> <ws33-192> hw.model: Intel(R) Xeon(R) CPU           E5645  @ 2.40GHz
> ```


## Запрет на выполнение деструктивных команд {#destructive}

Деструктивной называется команда, которая запускается в нескольких ДЦ на более чем 1000 хостов одновременно и имеет хотя бы один из признаков:
- запускается от имени суперпользователя (`root`);
- содержит команду `sudo` (проверяется наличие слова <q>sudo</q> с последующим пробелом в любой части команды);
- запускается без [porto-изоляции](https://wiki.yandex-team.ru/porto).

При запуске `sky run` выполнение деструктивной команды не будет запущено. Вернется предупреждение с рекомендациями по дальнейшим действиям. Вы можете запустить пошаговое выполнение команды (параметр [--step](#step) или последовательно запускать `sky run` в каждом из ДЦ.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky run -p "sudo less /var/log/skynet/copier.log" G@ALL_RUNTIME
> ```
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> ================================================================================
> WARNING! You're going to run sudo command in more than one DC.
> Please run this command per DC, for instance, using d@ prefix:
>    sky run "sudo less /var/log/skynet/copier.log" [G@ALL_RUNTIME] . d@sas
>  or using --step option:
>    sky run --step=100 "sudo less /var/log/skynet/copier.log" [G@ALL_RUNTIME]
> 
> Available DCs are: sas, man, vla, iva, myt
> ================================================================================
> 
> ```

#### Узнайте больше

* [Распространенные ошибки](https://wiki.yandex-team.ru/skynet/FAQ1/#naiboleeverojatnyeoshibkiichtosnimidelat)