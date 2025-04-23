# Удаленный доступ (sky shell)

Удаленный доступ к указанному [хосту](glossary.md#host) средствами Сqudp (опционально — выполнение команды на удаленном хосте).

Принцип соединения аналогичен используемому в SSH.

Если указана команда, которую необходимо выполнить, соединение с хостом будет закрыто после выполнения. В противном случае пользователю предоставляется доступ к командной оболочке на указанном хосте.

[Формат запуска](sky-shell.md#request-format)
[Формат вывода](sky-shell.md#response-format)
[Распространенные ошибки (Вики)](https://wiki.yandex-team.ru/skynet/FAQ2/#naiboleeverojatnyeoshibkiichtosnimidelat)

См. также раздел [CQueue / CQudp](https://doc.yandex-team.ru/Search/skynet-desc/concepts/public-services_cqueue.html) документа [Skynet. Общее описание](https://doc.yandex-team.ru/Search/skynet-desc/).

## Формат запуска {#request-format}

```
sky shell [опциональные ключи] <хост> ['команда']
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
Параметры вывода

|| `-v, --verbose` | Увеличить уровень вывода служебной информации в результате выполнения команды.

Требуемый уровень можно регулировать с помощью повтора ключа в команде.

Например, один ключ `-v` инициирует вывод первого уровня служебной информации, по ключу `-vvv` вернется служебная информация первого, второго и третьего уровня. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-q, --quiet` | Уменьшить уровень вывода служебной информации в результате выполнения команды.

Требуемый уровень можно регулировать с помощью повтора ключа в команде.

Например, один ключ `-q` уменьшает количество вывода служебной информации на один уровень, ключ `-qq` — на два уровня. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||
|#

**Хосты, инстансы, шарды и/или группирующие объекты, на которых должна выполняться команда**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** ||

|| `хост` | Хост, с которым необходимо установить соединение. | Обязательный.
|#

**Устаревшие. Обеспечивают обратную совместимость**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** ||

|| `--cqudp` | Использовать транспорт cqudp. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--cqueue_implementation=<тип транспорта>` | Использовать указанный тип транспорта. Единственное поддерживаемое значение ['cqudp'] | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|#

{% endcut %}


## Формат вывода {#response-format}

{% include [response-format-response-format-depends-on](_includes/sky-list/id-response-format/response-format-depends-on.md) %}


- [Командная оболочка на указанном хосте](#shell-on-remote-server) (команда не указана).
- [Вывод команды](#exec-result) (команда указана).

### Командная оболочка на указанном хосте {#shell-on-remote-server}

Возвращается, если не указана команда, которую необходимо выполнить на заданном хосте.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky shell ws6-034
> ```
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> skynet@ws6-034:~$
> ```

### Вывод команды {#exec-result}

Возвращается, если указана команда, которую необходимо выполнить на заданном хосте. После выполнения команды соединение с указанным хостом закрывается.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky shell ws6-034 'sysctl hw.model'
> ```
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> hw.model: Intel(R) Xeon(R) CPU           E5440  @ 2.83GHz
> 
> Connection closed by remote host.
> ```

#### Узнайте больше

* [Распространенные ошибки](https://wiki.yandex-team.ru/skynet/FAQ1/#naiboleeverojatnyeoshibkiichtosnimidelat)