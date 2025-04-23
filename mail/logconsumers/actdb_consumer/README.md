# Act_db consumer

Трекинг пользовательской активности на базе userjournal. Обновляет дату последней активности.

Консьюмер читает топик [userjournal/mail-user-journal-log][1]
и пишет в базу [act_db.history.user_activity][5] дату последней активности пользователя по модулям.

<details>
   <summary>Пример</summary>

      act_db=> select * from history.user_activity where uid='123456789';
         uid    |    module     |  last_dt
      ----------+---------------+------------
      123456789 | hound         | 2021-10-12
      123456789 | jsintegration | 2021-10-14
      123456789 | mailbox_oper  | 2021-10-12
      123456789 | mobile        | 2021-10-14
      123456789 | sendbernar    | 2021-10-12
      123456789 | spam_report   | 2021-09-16
      123456789 | yserver_imap  | 2021-10-14
      (7 rows)

</details>


## Deploy

Разворачивается [на 5 юнитах по 2 пода][2] в разных ДЦ. Запускается с параметром `--endpoint` для чтения из локальных партиций логброкера. Поскольку в MAN нет квоты, отдельным юнитом запущен `actdb-man`. Деплой автоматический после коммита в аркадийный trunk.

Другие параметы:

`--max-messages` — максимальное количество сообщений при чтении из топика.

`--flush-messages` — минимальное количество сообщений для записи в базу.


## Monitoring

Метрики доступны [на панели в головане][3].

Алерт на превышение порога последнего чтения либо лагу чтения [в джагглер][4].


## Production vs Development

В продакшне приложение авторизуется в логброкере [сервисным TVM-тикетом][7]. В разработке — OAuth токеном.
Нет ограничений на запуск на локальной машине, если есть доступ на чтение топика, запись в базу и сетевые доступы:

```(bash)
LOGBROKER_TOKEN=... DB_USER=... DB_PASS=... ./actdb_consumer \
   --endpoint iva.logbroker.yandex.net \
   --topic userjournal/mail-user-journal-log \
   --consumer shared/userjournal \
   --max-messages 10 \
   --flush-messages 10
```

Боевые секреты лежат [в секретнице][6].


[1]: <https://logbroker.yandex-team.ru/logbroker/accounts/userjournal/mail-user-journal-log?page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&consumer=shared%2Fuserjournal&metricsFrom=1634421816041&metricsTo=1634508216041&sortOrder=%22default%22> "logbroker read statistics"
[2]: <https://deploy.yandex-team.ru/stages/mail_logconsumer_production/status> "deploy stage"
[3]: <https://yasm.yandex-team.ru/template/panel/mail_actdb_consumer/?embed=1> "панель в головане"
[4]: <https://juggler.yandex-team.ru/raw_events/?query=tag%3Dmail-actdb-logconsumer__> "события в juggler"
[5]: <https://yc.yandex-team.ru/folders/foom5upuus069lavolqb/managed-postgresql/cluster/mdb0r5flaekksgta4v3j?section=overview> "база в MDB"
[6]: <https://yav.yandex-team.ru/secret/sec-01fhwrakf2j6gw9eg7svwb56pw/explore/versions> "секреты"
[7]: <https://abc.yandex-team.ru/services/maillogconsumer/resources/?view=consuming&layout=table&supplier=14&show-resource=27465841> "TVM-приложение"
