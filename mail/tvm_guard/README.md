**Что это**

Библиотека для управления доступами по TVM2 тикетам

**Примеры**

Лежат в папке `example`

**Общая схема проверки**

В метод `tvm_guard::Guard::check` передаются аргументы:
* `path` запроса
* юид из аргументов/хедеров/тела запроса
* опциональный сервисный тикет из заголовка `X-Ya-Service-Ticket`
* опциональный юзер тикет из заголовка `X-Ya-User-Ticket`

Метод возвращает `tvm_guard::Response`, по которому можно либо пропустить запрос дальше, либо отклонить его

**tvm_guard::Response**

Результат проверки запроса.
Обязательные поля:
* `action` - пропускать ли запрос
* `reason` - причина почему вернули такой `action`

Опциональные поля:
* `error` - код ошибки
* `source` - src tvm id из сервистикета
* `uidsFromUserTicket` - юиды из юзертикета
* `issuerUid` - юид из рутового сервистикета
* `defaultUid` - дефолтный юид из юзертикета

**Рутовый сервисный тикет**

Отладку запросов можно осуществлять с помощью рутового приложения.
Заводится особый сервис в abc, для него выписывается tvm приложение, айди которого можно прописать в конфиге. Все запросы с сервис тикетом этого приложения будут пропускаться. Сервисные тикеты должны быть выписаны с помощью ssh-подписи. Иначе в них не будет `issuer_uid` - корпового юида пользователя, который выписал сервисный тикет. Сейчас используется одно такое приложение https://abc.yandex-team.ru/services/javatests/


**tvm_curl**

Для упрощения выписывания рутовых сервисных тикетов существует [`tvm_curl`](https://a.yandex-team.ru/arc/trunk/arcadia/mail/tvm_guard/tool): обёртка над паспортной утилитой `tvmknife` и `curl`. В утилиту зашит tvmid из [приложения](https://abc.yandex-team.ru/services/javatests/), от имени которого выписывается сервисный тикет. В качестве dst берётся tvmid из переменных среды или из файла `/tvm2_root_client_id`.


**tvm_guard::Action**

Может быть `reject` (запрос должен быть отклонён) и `accept` (запрос можно пропускать дальше)

**tvm_guard::Reason**

Причина почему вернули такой `tvm_guard::Action`:
* `defaultPolicy` - не нашли для ручки правило, ответили дефолтом для всего сервиса
* `rootServiceTicket` - рутовый тикет
* `rootServiceTicketWithoutUid` - проблемы с рутовым сервисным тикетом
* `rule` - для ручки нашли правило и смогли проверить тикеты
* `ruleDefaultPolicy` - для ручки нашли правило, но какие-то проблемы с тикетами
* `uidsMismatch` - юид из юзертикета не совпадает с переданным на проверку юидом
* `unknownService` - в конфиге нет такого tvm приложения
* `wrongServiceTicket` - невалидный сервисный тикет
* `wrongUserTicket` - невалидный юзер тикет


Вместе с `tvm_guard::Action::accept` могут быть такие причины: [`rootServiceTicket` , `rule` , `ruleDefaultPolicy` , `defaultPolicy`]
Вместе с `tvm_guard::Action::reject` могут быть такие причины: [`wrongServiceTicket`,  `wrongUserTicket`,  `uidsMismatch`,  `rootServiceTicketWithoutUid`,  `rule`,  `ruleDefaultPolicy`,  `defaultPolicy`,  `unknownService`]


**Клиенты**

Пары из человекочитаемых названий и tvm id

**Правила**

Библиотека оперирует правилами. Правило имеет человекочитаемое имя, список путей, для которых оно применимо, дефолтный ответ и два списка клиентов: клиенты, для которых достаточно сервис тикета, и клиенты, от которых требуются сервис и юзер тикеты.
Правила применяются по порядку, в котором они описаны в конфиге.
Если какой-то один путь применим для нескольких правил, то запуск сервиса с такими правилами прервется с сообщением об ошибке.
Больше информации о применении правил можно узнать в тестах https://a.yandex-team.ru/arc/trunk/arcadia/mail/tvm_guard/tests

**Строгая проверка юидов**

Если она включена, то переданный на проверку юид из запроса должен присутствовать в списке юидов из юзер тикета. Нельзя будет передать любой валидный юзертикет для юида А и юид Б в запросе.

**Конфигурирование**

```
bb_env: blackbox
default: reject
strong_uid_check: true
root_client_id: 10
clients:
-   name: service1
    id: 1000
-   name: service2
    id: 1001
rules:
-   name: send
    paths: ['/default_reject']
    default_action: reject
    accept_by_service: ['service2']
    accept_by_user: ['service1']
-   name: compose
    paths: ['/default_accept']
    default_action: accept
    accept_by_service: []
    accept_by_user: ['service1']
-   name: reject_all
    paths: ['/reject_all']
    default_action: reject
    accept_by_service: []
    accept_by_user: []
```

* `bb_env` - какой ЧЯ (прод, корп, тестинг) используется (параметр прокидывается в `ymod_tvm`)
* `default` - что отвечать если для ручки не смогли найти правило
* `strong_uid_check` - включать ли строгую проверку юидов
* `root_client_id` - tvm id для рутового приложения
* `clients` - список клиентов
* `rules` - список правил

**Логирование**

Библиотека содержит хелперы для обычного неструктурированного логирования `tvm_guard/log_simple.h` и для логирования в `tskv` через LOGDOG `tvm_guard/log_tskv.h`

**Yplatform модули**

Для упрощения работы с `tvm_guard` в библиотеке есть интерфейс `tvm_guard::Module` для yplatform
Интерфейс модуля:
* `bind` - хелпер, который принимает на вход ссылку на `ymod_webserver::server` и поля, которые прокидывает в `ymod_webserver::server::bind`. Пользовательский хендлер сохраняется в обёртку, которая проверяет можно ли пропускать запрос. В случае успеха проверки хендлер вызывается, в случае неудачи отвечается `401 Unauthorized` с текстовым телом ответа `tvm_guard::Reason` 
* `check` - проверяет можно ли пропускать запрос

```
auto serverModule = yplatform::find<ymod_webserver::server>("webserver");
auto guardModule = yplatform::find<tvm_guard::Module>("tvm_guard");

guard->bind(*server, "", {"/ping"}, [] (ymod_webserver::response_ptr stream) {
	stream->result(ymod_webserver::codes::ok, "pong");
});
```

*Модуль tvm_guard::Dummy*

Тупой модуль, который пропускает или запрещает все запросы. Нужен если нужно срочно закрыть или открыть сервис по tvm.

```
-   _name: tvm_guard
    system:
        name: tvm_guard
        factory: tvm_guard::Dummy
    configuration:
		logger:
			guard: tvm_guard_log
			module: application_log
		default_action: accept
```

* `logger.guard` - лог для логирования результатов проверки
* `logger.module` - модуль для логирования информации о работе модуля
* `default_action` - пропускать или запрещать ли запосы


*Модуль tvm_guard::WithYModTvm*

Модуль для проверки запросов с помощью `tvm_guard` и `ymod_tvm`

```
-   _name: tvm_guard
    system:
        name: tvm_guard
        factory: tvm_guard::WithYModTvm
    configuration:
        dependencies:
            tvm: ymod_tvm
		logger:
			guard: tvm_guard_log
			module: application_log
		guard: ...
```

* `dependencies.tvm` - имя `ymod_tvm` модуля
* `logger.guard` - лог для логирования результатов проверки
* `logger.module` - модуль для логирования информации о работе модуля
* `default_action` - пропускать или запрещать ли запосы
* `guard` - основная конфигурация библиотеки 

Реазилация метода `check` берёт параметр `uid` из GET-параметров.

