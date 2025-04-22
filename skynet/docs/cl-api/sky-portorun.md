# Выполнение команды в контейнерах porto (sky portorun)

Выполнение произвольной команды в porto-контейнерах.

Авторизация осуществляется посредством [portoshell](sky-portoshell.md). Запуск команды  возможен только в контейнерах с префиксом `f@`.

На хосте, с которого запускается, должны быть запущены демоны Cqudp и Portoshell.

[Формат запуска](sky-portorun.md#request-format)
[Формат вывода](sky-portorun.md#response-format)
[Распространенные ошибки (Вики)](https://wiki.yandex-team.ru/skynet/FAQ2/#naiboleeverojatnyeoshibkiichtosnimidelat)

## Формат запуска {#request-format}

```
sky portorun [опциональные ключи] 'команда' <контейнер>
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

|| `--data-limit=<максимальный размер данных>` | Ограничивать размер возвращаемого сервером ответа.

В значении ключа указывается максимально допустимое значение в мегабайтах. Если ключ не задан, действует ограничение в один мегабайт. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||
|#

**Группирующие объекты, на которых должна выполняться команда**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** ||

||`контейнер` | Имя контейнера (слот), в котором необходимо выполнить команду.

Указывается в виде выражения [калькулятора Блинова](https://doc.yandex-team.ru/generated/skynet/sky/blinovcalc.html) с префиксом `f@`. | Обязательный. ||
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


- [Компактный](#compact-mode-response) (ключ [`--stream`](#stream-row) отсутствует).
- [Потоковый](#stream-response-format) (ключ [`--stream`](#stream-row)).

### Компактный {#compact-mode-response}

Возвращается, если отсутствует ключ [`--stream`](#stream-row).

Объекты (контейнеры), для которых результаты выполнения команды совпадают, группируются.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky portorun -p "uname -a" f@test_service_for_torkve
> ```
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> 3 / 3 |####################################################################################################################| Elapsed Time: 0:00:06
> ================================================================================
> Success on slots(s) (u'sas1-4205.search.yandex.net', '28636@sas1-4205.search.yandex.net', '')
> --------------------------------------------------------------------------------
> Linux sas1-4205-sas-skynet-experiment-porto-28636.gencfg-c.yandex.net 4.4.114-50 #1 SMP Fri Feb 2 10:53:13 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
> 
> ================================================================================
> 
> ================================================================================
> Success on slots(s) (u'sas1-8549.search.yandex.net', '28636@sas1-8549.search.yandex.net', '')
> --------------------------------------------------------------------------------
> Linux sas1-8549-020-sas-skynet-exper-b89-28636.gencfg-c.yandex.net 4.4.114-50 #1 SMP Fri Feb 2 10:53:13 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
> 
> ================================================================================
> 
> ================================================================================
> Success on slots(s) (u'sas1-7903.search.yandex.net', '28636@sas1-7903.search.yandex.net', '')
> --------------------------------------------------------------------------------
> Linux sas1-7903-sas-skynet-experiment-porto-28636.gencfg-c.yandex.net 4.4.162-68 #1 SMP Fri Oct 26 15:44:52 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
> 
> ================================================================================
> 
> ```

### Потоковый {#stream-response-format}

Возвращается, если указан ключ [`--stream`](#stream-row).

Возвращает ответы от объектов (контейнеров) по мере получения. Результаты разделены символом переноса строки.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky portorun --stream "uname -a" f@test_service_for_torkve
> ```
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> <(u'sas1-1354.search.yandex.net', '28636@sas1-1354.search.yandex.net', '')> Linux sas1-1354-sas-skynet-experiment-porto-28636.gencfg-c.yandex.net 4.4.114-50 #1 SMP Fri Feb 2 10:53:13 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
> <(u'sas1-9227.search.yandex.net', '28636@sas1-9227.search.yandex.net', '')> Linux sas1-9227-sas-skynet-experiment-porto-28636.gencfg-c.yandex.net 4.4.162-68 #1 SMP Fri Oct 26 15:44:52 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
> <(u'sas1-9360.search.yandex.net', '28636@sas1-9360.search.yandex.net', '')> Linux sas1-9360-sas-skynet-experiment-porto-28636.gencfg-c.yandex.net 4.4.114-50 #1 SMP Fri Feb 2 10:53:13 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
> ```

#### Узнайте больше

* [Распространенные ошибки](https://wiki.yandex-team.ru/skynet/FAQ1/#naiboleeverojatnyeoshibkiichtosnimidelat)