### Основы работы с сервисом

CallMeBack - это сервис, который позволяет зарегистрировать отложенное до указанного времени событие.
Когда наступает указанный момент, сервис оповещает потребителя способом, который он указал при создании события
(например, HTTP-запросом).

Список ручек HTTP-интерфейса сервиса можно посмотреть в [Swagger].
Там же можно их и попробовать. В этом документе "человеческим языком" описано то, что не уместилось в непосредственном
описании ручек.

#### Глоссарий
Вот краткое обьяснение терминов, используемых в интерфейсе сервиса.

##### `X-Ya-Service-Ticket`
HTTP-заголовок, в котором содержится [сервисный TVM-тикет](https://wiki.yandex-team.ru/passport/tvm2/stbrief/).

При создании события, `src:client_id` из этого тикета (или факт его отсутствия) запоминается
вместе с остальной информацией о событии. При этом:
* При HTTP-нотификации потребителя, если при создании события был передан тикет, CallMeBack формирует сервисный тикет
  от имени [Worker сервиса напоминаний](https://abc.yandex-team.ru/services/remindersservice/resources/) соответствующего
  окружения и добавит его в HTTP-хедер. В `dst` тикета будет `client_id` того сервиса, который создал событие.
* Любые ручки, работающие с информацией о событиях, также принимают тикет и учитывают только события, созданные тем же клиентом.
  Таким образом, CallMeBack логически изолирует потребителей друг от друга.


##### `group_key`
Внешний (задающийся потребителем) ключ, логически объединяющий набор событий.
Например, идентификатор пользователя сервиса-потребителя.

С помощью `group_key` можно запрашивать информацию о списке событий.

##### `event_key`
Внешний (задающийся потребителем) ключ, идентифицирующий конкретное событие.
Позволяет после создания события запрашивать его статус или отменять его.

Должен быть уникальным в пределах одного `group_key` (а также одного `client_id`).
Создание события с уже использованными `group_key, event_key` отклоняется сервисом.

##### `context`
Произвольные JSON-данные, которые можно получить в ручках информации о событиях и/или в нотификации от CallMeBack.

##### `retry_params`
Опциональный параметр из context.
Позволяет клиенту настраивать политику ретраев.
Возможные поля:
* stop_after_delay: задает интервал в секундах, после которого событие считается протухшим
  и больше не пытается выполнится(переводится в состояние failed), по умолчанию 5 дней;
* quick_retries_count: задает количество быстрых ретраев(т.е. быстрых ретраев без решедулинга в базе), по умолчанию 5,
  чтобы не использовать быстрые ретраи надо задать 0;
* strategy: задает тип стратегии основных ретраев(с решедулингом в базе), сейчас реализованы стратегии "constant" и "exponential",
  если параметр не задан то используется по умолчанию "constant" стратегия с base_delay=60с;
* base_delay: базовая задержка между ретраями, обязательный параметр если задана стратегия ретраев;
* delay_growth_rate: коэффициент роста задержки между ретраями для "exponential" стратегии,
  обязательный параметр если задана "exponential" стратегия ретраев;
Пример:
context = '{"retry_params": {"quick_retries_count": 0, "strategy": "exponential", "base_delay": 60, "delay_growth_rate": 2}}'

 Для того, чтобы получить нужные данные в нотификации, необходимо при создании задать правильную схему нотификации:
##### `notify_scheme`
Описывает, как именно CallMeBack будет нотифицировать сервис-потребитель о событии. Задает транспорт и формат сообщения.
Возможные значения указаны в описании
 [ручки создания события](http://callmeback-test.mail.yandex.net/api/doc#!/Api/post_v1_add) в [Swagger].

#### Что здесь надо делать?

Используем ручку создания события, обязательно передаем ей туда:
* время, на которое планируется нотификация;
* url, по которому нужно будет связаться с потребителем.

При желании, используем TVM-тикеты. **N.B.** Сейчас для работы с TVM необходимо прописать `client_id` потребителя в конфиг
CallMeBack, т.к. он живет в Qloud и пользуется TVM-демоном, у которого такие требования.

Если хотим опрашивать состояние события и/или иметь возможность отменить его - указываем `group_key` и `event_key`.

При необходимости, добавляем контекст и нестандартную схему нотифицирования.

Готово, вы восхитительны. _**Мы вам перезвоним.**_

[Swagger]: http://callmeback-test.mail.yandex.net/api/docs
