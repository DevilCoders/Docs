# Удаленный доступ к контейнерам porto (sky portoshell)

Удаленный доступ к указанному [porto-контейнеру](https://wiki.yandex-team.ru/porto/) средствами Сqudp (опционально — выполнение команды в porto-контейнере).

{% include [commands-keys-require-cqudp](_includes/commands-keys/id-commands-keys/require-cqudp.md) %}


Принцип соединения аналогичен используемому в SSH. У пользователя должен быть доступ к хосту на порт 10045.

Если указана команда, которую необходимо выполнить, соединение с контейнером будет закрыто после выполнения. В противном случае пользователю предоставляется доступ к командной оболочке в указанном контейнере.

[Формат запуска](sky-portoshell.md#request-format)
[Формат вывода](sky-portoshell.md#response-format)
[Распространенные ошибки (Вики)](https://wiki.yandex-team.ru/skynet/FAQ2/#naiboleeverojatnyeoshibkiichtosnimidelat)

См. также информацию о Portoshell в [Вики](https://wiki.yandex-team.ru/Skynet/Services/Portoshell/).


## Формат запуска {#request-format}

```
sky portoshell [опциональные ключи] <контейнер> ['команда']
```

{% cut "Возможные ключи и значения" %}

**Параметры аутентификации**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** ||

|| `-i <путь до файла>` | Использовать пользовательский ключ, доступный в указанном файле.
Аналог команды , выполняемой с ключом `-i`. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-u <имя пользователя>`, 
`--user=<имя пользователя>` | Выполнять команду от имени указанного пользователя.

Cм. раздел [Аутентификация](https://doc.yandex-team.ru/Search/skynet-desc/concepts/authentication.html) документа [Skynet. Общее описание](https://doc.yandex-team.ru/Search/skynet-desc/) | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||
|#

**Параметры запуска и выполнения**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** ||

|| `-p <номер порта>`, 
`--port=<номер порта>` | Использовать указанный порт для доступа на сервер. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--env=<ключ=значение>` | Задать пользовательскую переменную окружения. Переменная действует в рамках текущей сессии.

Экранировать специальные символы в значении переменной не требуется. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `--unset-env=<ключ>` | Удалить пользовательскую переменную окружения в рамках текущей сессии. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-I, --interactive` | Включить интерактивный режим работы с терминалом. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-C <идентификатор конфигурации>`, 
`--configuration-id=<идентификатор конфигурации>` | Использовать указанную конфигурацию. Если ключ не задан, соединение устанавливается с активной конфигурацией. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| `-t <значение>`, 
`--timeout=<значение>` | Ограничить время ожидания команды. Если в течение указанного времени, команда не поступила, сессия с контейнером закроется.

Значение задается в секундах. | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|| **Команда к выполнению** ||

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

**Группирующие объекты, на которых должна выполняться команда**

#|
|| **Ключ** | **Описание** | **Признак обязательности, ограничения** ||

|| `контейнер` | Имя контейнера (слот), с которым необходимо установить соединение.

По умолчанию соединение устанавливается с активной конфигурацией в контейнере. Если необходима определенная конфигурация, то ее надо указать в формате:`<контейнер:идентификатор конфигурации>`.

Если указанный контейнер не найден, команда вернет список доступных контейнеров на хосте. | Обязательный. ||

|| `-H <имя хоста>, --host=<имя хоста>` | Имя хоста, на котором размещен контейнер.

Если параметр не задан, предполагается, что контейнер указан в формате `<сервис@хост>` | 

{% include [commands-keys-non-obligatory](_includes/commands-keys/id-commands-keys/non-obligatory.md) %} ||

|#

{% endcut %}

## Формат вывода {#response-format}

{% include [response-format-response-format-depends-on](_includes/sky-list/id-response-format/response-format-depends-on.md) %}


- [Командная оболочка на указанном хосте](#shell-on-remote-server) ( команда не указана).
- [Вывод команды](#exec-result) (команда указана).

### Командная оболочка на указанном хосте {#shell-on-remote-server}

Возвращается, если не указана команда, которую необходимо выполнить на заданном хосте.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky portoshell 28636@sas1-1354.search.yandex.net
> ```
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> root@sas1-1354-sas-skynet-experiment-porto-28636:/place/db/iss3/instances/28636_test_service_for_torkve_HIYQki1vgjH#
> ```

### Вывод команды {#exec-result}

Возвращается, если указана команда, которую необходимо выполнить на заданном хосте. После выполнения команды соединение с указанным хостом закрывается.

> {% include [response-format-the-following-command](_includes/sky-list/id-response-format/the-following-command.md) %}
> 
> 
> ```
> sky portoshell 28636@sas1-1354.search.yandex.net "uname -a"
> ```
> 
> {% include [response-format-the-following-answer](_includes/sky-list/id-response-format/the-following-answer.md) %}
> 
> 
> ```
> Linux sas1-1354-sas-skynet-experiment-porto-28636.gencfg-c.yandex.net 4.4.114-50 #1 SMP Fri Feb 2 10:53:13 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
> 
> Connection closed by remote host.
> ```

#### Узнайте больше

* [Распространенные ошибки](https://wiki.yandex-team.ru/skynet/FAQ1/#naiboleeverojatnyeoshibkiichtosnimidelat)