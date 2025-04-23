# Версия Skynet (sky version)

Возвращает сведения о версии {{ serviceName }}, установленной на указанных хостах.

{% note info %}

Для вывода информации о версии {{ serviceName }}, установленной на текущем хосте, необходимо выполнить команду  с ключом `--version`.

{% endnote %}

[Формат запуска](sky-svninfo.md#request-format)
[Формат вывода](sky-svninfo.md#response-format)
[Распространенные ошибки (Вики)](https://wiki.yandex-team.ru/skynet/FAQ2/#naiboleeverojatnyeoshibkiichtosnimidelat)

## Формат запуска {#request-format}

```
sky version [опциональные ключи] <xосты и/или группирующие объекты>
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

|| `--svn` | Возвращать путь до исходников в SVN и номер ревизии установленной версии Skynet вместо явного указания номера версии. |

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||
|#

**Хосты и/или группирующие объекты, на которых должна выполняться команда**

{% note alert %}

Требуемые хосты и/или группы должны быть указаны только одним из доступных способов.

{% endnote %}

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** || 

|| `хосты и/или группирующие объекты` | Список хостов и/или группирующих объектов, на хостах которых необходимо выполнять команду.
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

Результаты выполнения группируются по хостам, для которых версия {{ serviceName }} совпадает.

{% include [response-format-response-format-depends-on](_includes/sky-list/id-response-format/response-format-depends-on.md) %}


- [Стандартный](#standard).
- [Путь до исходников в SVN и номер ревизии](#svn-key) (ключ [`--svn`](#svn-row)).

### Стандартный {#standard}

Возвращается, если не указан ключ [`--svn`](#svn-row).

Содержит сведения о версии {{ serviceName }}, установленной на указанных хостах. Хосты, для которых результаты выполнения команды совпадают, группируются.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky version -l h@imgs1-{032,037,044,050,051} h@ws9-{512,513}
> ```
> 
> Версии {{ serviceName }}, установленные на указанные хосты, совпадают.
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> ================================================================================
> Success on 7 host(s): +imgs1-{032,037,044,050,051}.yandex.ru +ws9-{512,513}.yandex.ru
> --------------------------------------------------------------------------------
> 9.20.5
> ================================================================================
> ```

### Путь до исходников в SVN и номер ревизии {#svn-key}

Возвращается, если указан ключ [`--svn`](#svn-row).

Содержит сведения о пути до исходников установленной версии {{ serviceName }} в репозитории, а также соответствующей ревизии.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky version --svn h@ws39-049 h@ws40-157
> ```
> 
> {% include [response-format-skynet-versions-are-identical](_includes/sky-svninfo/id-response-format/skynet-versions-are-identical.md) %}
> 
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> ================================================================================
> Success on 2 host(s): +ws39-049 +ws40-157
> --------------------------------------------------------------------------------
> svn+ssh://arcadia.yandex.ru/arc/branches/skynet/release-10.14@1357327
> ================================================================================
> ```

#### Узнайте больше

* [Распространенные ошибки](https://wiki.yandex-team.ru/skynet/FAQ1/#naiboleeverojatnyeoshibkiichtosnimidelat)