# Регламент внутренних учений Директа

## Учения по закрытию сервисных машин (не участвуют БД, YT и т.п.)

{% note alert %}

Если загорается disaster алерт, значительно повышается фон 500-х или в тревожный чат приходят с жалобами &mdash; сразу возвращаем прежнюю нагрузку.

{% endnote %}

[Предыдущие отчеты](https://st.yandex-team.ru/issues/?_f=type+priority+key+summary+description+status+resolution+created+updated+assignee+parent+rootCause&_q=Queue%3A+DIRECTADMIN+Tags%3A+%22type%3Adrills%22+%22Sort+by%22%3A+Created+DESC) &mdash; можно посмотреть где закрывалось и закрывать следующую локацию по кругу.

### Инструкция

Один дежурный идет по инструкции, согласуя действия (при желании, ощущения) со вторым, например про критичность открытого инцидента, скидывая ссылки на заполненную форму, уход трафика.

1. Продакшен готов к учениям (если не готов &mdash; двигаем учения на час до следующего слота в интервале 12:00 &ndash; 18:00, затем переносим на следующий день):
    - Нет аварий в [Координация больших факапов](../reference/chats.md#global-incidents).
    - Нет активных инцидентов в Директе.
    - В мониторингах нет критичных срабатываний, 500-е в норме. Смотреть по дашборду [direct-group-sre-tv](https://solomon.yandex-team.ru/?project=direct&dashboard=direct-group-sre-tv).
1. Открыть дашборды и графики:
    - [direct-group-sre-tv](https://solomon.yandex-team.ru/?project=direct&dashboard=direct-group-sre-tv) &mdash; смотрим мониторинги, время ответа api и интерфейса, трафик, 500ки.
    - [Трафик по приложениям и ДЦ](https://monitoring.yandex-team.ru/projects/direct/dashboards/monfu62erm9fkta44nk7?from=now-1h&to=now&refresh=60000) &mdash; убеждаемся в том что трафик распределяется ожидаемо.
1. Написать в [Direct.Admin.Chat](../reference/chats.md#direct-admin-chat) "закрываю такой-то ДЦ на внутренние учения".
1. Закрыть сервисные машины:
    1. Увести трафик через L7Heavy из закрываемой локации &mdash; [инструкция](./howto-dc-l7.md).
    1. Снять анонсы балансеров в закрываемой локации (если применимо) &mdash; [инструкция](./howto-awacs-shutdown-announce.md).
    1. Закрыть сервисные машины <https://firewall.yandex-team.ru/drills/add>
        - Project &mdash; `_PPCNETS_`
        - ДЦ
        - Duration &mdash; 15 минут
        - Exclude:
          ```
          _C_MODERATE_PERL_
          _C_DIRECT_NG_MOD_DATABASES_MYSQL_PROD_
          _C_DIRECT_NG_MOD_DATABASES_MYSQL_MODLOG_
          ```
        **Кнопка для отмены учений раньше обозначенного срока появится после создания записи.**
1. Убедиться, что трафик ожидаемо перераспределился.
1. Смотрим 15 минут за графиками и мониторингами. **Если проблемы &mdash; открываем ДЦ раньше!**
1. Открыть сервисные машины:
    1. Дождаться открытия по таймеру или отменить учения.
    1. Вернуть анонсы балансеров в закрываемой локации.
    1. Вернуть трафик через L7Heavy в закрываемую локацию.
1. Убедиться, что трафик перераспределился обратно.
1. Убедиться, что мониторинги и 500-е в норме.
1. Прикрепить в тикет скриншоты графиков (данные в solomon прореживаются через некоторое время).
1. Записать в тикет важные наблюдения.
1. Проставить на тикет тег успешности (`result:success` или `result:fail`).

### Полезные графики

- [Отставание b2yt](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-b2yt&service=java-monitoring&l.sensor=time_lag&l.sync_state=stable&l.yt_cluster=seneca-sas&graph=auto&b=1h&e=&l.host=CLUSTER) (нужно выбрать кластер).
- [Выполнения джоб по хостам](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.sensor=quartz_running&graph=auto&host=!CLUSTER&b=1h&e=).
