# Копирование данных в (из) удаленного контейнера porto (sky portocopy)

Копирование данных между локальным сервером и удаленными [porto-контейнерами](glossary.md#container).

Является аналогом работы утилиты scp в UNIX-подобных операционных системах.

[Формат запуска](sky-portocopy.md#request-format)
[Формат вывода](sky-portocopy.md#response-format)
[Распространенные ошибки (Вики)](https://wiki.yandex-team.ru/skynet/FAQ2/#naiboleeverojatnyeoshibkiichtosnimidelat)

## Формат запуска {#request-format}

```
sky portocopy [опциональные ключи] [-C <идентификатор конфигурации>] [slot]:file1... [slot]:file2
```

{% cut "Возможные ключи и значения" %}

**Параметры аутентификации**

#|
||**Ключ** | **Описание** | **Признак обязательности, ограничения** || 

|| `-u <имя пользователя>`, 
`--user=<имя пользователя>` | Выполнять команду от имени указанного пользователя.

Cм. раздел [Аутентификация](https://doc.yandex-team.ru/Search/skynet-desc/concepts/authentication.html) документа [Skynet. Общее описание](https://doc.yandex-team.ru/Search/skynet-desc/) | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||
|#

**Параметры запуска и выполнения**

#|
||**Ключ** | **Описание** | **Признак обязательности, ограничения** || 

|| `-p <номер порта>, --port=<номер порта>` | Использовать указанный порт для доступа на сервер. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-C <идентификатор конфигурации>`, 
`--configuration-id=<идентификатор конфигурации>` | Использовать указанную конфигурацию. Если ключ не задан, соединение устанавливается с активной конфигурацией. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-r` | Рекурсивно копировать всю директорию. Если в копируемом каталоге присутствуют символьные ссылки, то в конечную директорию копируются не ссылки, а данные, на которые они указывают. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||
|#

**Хосты, porto-контейнеры, на которых должна выполняться команда**

#|
||**Ключ** | **Описание** | **Признак обязательности, ограничения** || 

|| `-H <имя хоста>, --host=<имя хоста>` | Имя хоста, на котором размещен контейнер.

>Если параметр не задан, предполагается, что контейнер указан в формате `<сервис@хост>` | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||
|#

{% endcut %}

## Формат вывода {#response-format}

В случае успешного завершения возвращается информация о результатах выполнения команды. При проявлении ошибок по крайней мере на одном из хостов возвращается информация об ошибке.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky portocopy loop.log 28636@sas1-0928.search.yandex.net:loop2.log
> ```
> 
> Команда копирует локально расположенный файл в удаленный контейнер.
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> loop.log 100% 961KB 961.2KB/s 00:00
> ```

#### Узнайте больше

* [Распространенные ошибки](https://wiki.yandex-team.ru/skynet/FAQ1/#naiboleeverojatnyeoshibkiichtosnimidelat)