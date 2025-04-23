## MediascopeSettingsRefresherJob

### Продукт/подсистема

Интеграция Директа с верификаторами рекламы.


### Роль в работе продукта/подсистемы

Отвечает за поддержание актуальности клиентских токенов для доступа в апи Mediascope. Токены нужны для синхронизации баннеров с пикселями Mediascope с их личным кабинетом.


### Датафлоу

- Собирает из базы (таблица [client_measurers_settings](https://direct-dev.yandex-team.ru/db/ppc/tables/client_measurers_settings.html)) близкие к протуханию токены
- Обновляет токены в Mediascope через их API.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.MediascopeSettingsRefresherJob.working.production&last=1DAY&query=)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'clientmeasurersettings.MediascopeSettingsRefresherJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Критично. У пользователей протухнет авторизация в Mediascope, их баннеры перестанут синхронизироваться, и пользователям нужно будет заново авторизоваться через интерфейс Директа и надо будет перепослать неотправленные баннеры.


### Как пользователи (или команда) заметят проблему и через какое время

У пользователей не появятся новые баннеры Директа в личном кабинете Mediascope.


### Контакты разработчиков и менеджеров

Разработчики: [Егор Иватько](https://staff.yandex-team.ru/ivatkoegor) <br/>
Менеджеры: [Алексей Александров](https://staff.yandex-team.ru/hrustyashko)


### Желательное время исправления в случае поломки

Главное выяснить на чьей стороне поломка - на нашей или на стороне Mediascope. Если на нашей, то чинить asap.


### Способы регулирования работы джобы

Настройка времени протухания токена (через которое его нужно обновить) лежит в константе `EXPIRATION_PERIOD_IN_SECONDS` в [коде джобы](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/java/ru/yandex/direct/jobs/clientmeasurersettings/MediascopeSettingsRefresherJob.java).


### Известные причины поломок

Может отвалиться АПИ на стороне Mediascope, в логах это выглядит примерно так:  <br/>
`Sending request get_prefix to Mediascope|Exception: java.util.concurrent.ExecutionException: java.net.ConnectException: Network is unreachable: partners.mediascope.net/194.190.21.20:443`

Алгоритм действий в случае проблем:
1. Выяснить какой сервис недоступен. Если недоступен `partners.mediascope.net`, то можно чинить в рабочее время в течение пары дней, если недоступен `auth.mediascope.net`, то нужно чинить ASAP.
2. Проверить, что проблема на стороне Mediascope, выполнив команды (со своего компьютера и с сервера):
    * `nc -vz partners.mediascope.net 443`<br/>
      Ожидаемый вывод: `Connection to partners.mediascope.net 443 port [tcp/https] succeeded!`

    * `nc -vz auth.mediascope.net 443`<br/>
      Ожидаемый вывод: `Connection to auth.mediascope.net 443 port [tcp/https] succeeded!`

   Если вывод отличается от ожидаемого, связаться с круглосуточным дежурным в Mediascope по контактам: тел.: +7 495 935-8718 доб. 2547, e-mail: duty@mediascope.net. Пример сообщения: "Здравствуйте, это Яндекс.Директ, мы интегрируемся с вашим API partners.mediascope.net для передачи рекламных позиций в личный кабинет. Видим фон 500-ок от хоста <проблемный хост>. Подскажите, пожалуйста, примерные сроки починки."
3. В случае недоступности `auth.mediascope.net`, завести тикет по [шаблону](https://st.yandex-team.ru/createTicket?queue=DIRECT&description=**%D0%9A%D0%BE%D0%B3%D0%B4%D0%B0%3A**%0A%D0%BF%D0%BE%D1%81%D0%BB%D0%B5+%D0%BF%D0%BE%D1%87%D0%B8%D0%BD%D0%BA%D0%B8+%3CID+%D1%82%D0%B8%D0%BA%D0%B5%D1%82%D0%B0+%D0%BF%D1%80%D0%BE+%D0%B0%D0%B2%D0%B0%D1%80%D0%B8%D1%8E%3E%0A%0A**%D0%A7%D1%82%D0%BE+%D0%B4%D0%B5%D0%BB%D0%B0%D0%B5%D0%BC%3A**%0A%D0%9F%D1%80%D0%B8+%D0%BD%D0%B0%D0%BB%D0%B8%D1%87%D0%B8%D0%B8+%D0%BD%D0%B5%D0%B2%D0%B0%D0%BB%D0%B8%D0%B4%D0%BD%D1%8B%D1%85+%D1%82%D0%BE%D0%BA%D0%B5%D0%BD%D0%BE%D0%B2%2C+%D0%BF%D1%80%D0%B8%D0%B7%D0%B2%D0%B0%D1%82%D1%8C+%3C%D0%BB%D0%BE%D0%B3%D0%B8%D0%BD+%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80%D0%B0%3E+%D0%B4%D0%BB%D1%8F+%D1%83%D0%B2%D0%B5%D0%B4%D0%BE%D0%BC%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F+%D0%BA%D0%BB%D0%B8%D0%B5%D0%BD%D1%82%D0%BE%D0%B2.%0A%0A**%D0%97%D0%B0%D0%BF%D1%80%D0%BE%D1%81+%D0%B4%D0%BB%D1%8F+%D0%BF%D0%BE%D0%B8%D1%81%D0%BA%D0%B0+%D0%BD%D0%B5%D0%B2%D0%B0%D0%BB%D0%B8%D0%B4%D0%BD%D1%8B%D1%85+%D1%82%D0%BE%D0%BA%D0%B5%D0%BD%D0%BE%D0%B2%3A**%0A%25%25direct-sql+pr%3Appc%3Aall+%22select+ClientID%2C+JSON_EXTRACT%28settings%2C+%27%24.expires_at%27%29+from+client_measurers_settings+where+JSON_EXTRACT%28settings%2C+%27%24.expires_at%27%29+%3C+UNIX_TIMESTAMP%28%29%22%25%25&priority=2&summary=MediascopeSettingsRefresherJob.+%D0%9F%D0%BE%D0%B8%D1%81%D0%BA+%D0%BD%D0%B5%D0%B2%D0%B0%D0%BB%D0%B8%D0%B4%D0%BD%D1%8B%D1%85+%D1%82%D0%BE%D0%BA%D0%B5%D0%BD%D0%BE%D0%B2&tags%5B%5D=app-duty-postponed-action&type=2)

### Дополнительно: тонкости и подводные камни

- [Внутренний инструмент](https://test-direct.yandex.ru/internal_tools/#mediascope_positions_send) для переотправки баннеров в Mediascope.
