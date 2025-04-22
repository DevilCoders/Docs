Логи пишутся на машинках, где крутится тач и льются в [YT](./links.md#Логи). В YT доступны дневные логи (доступны на следующий день), 30-минутные и 5-минутные (заливаются раз в 30 или 5 минут). Live-логи доступны только непосредственно на машинках. Погрепать их можно с помощью [executer](https://wiki.yandex-team.ru/executer/).

Логи пишут `nginx` и `duffman`. Последний пишет два вида логов `duffman-access` — все про запрос, статус запроса моделей, параметры запроса и т.п., `duffman-http` — все про http-запросы к бэкендам в пределах одного запроса. Во всех логах есть сквозной `request_id`, по нему можно добраться вплоть до логов на бэкендах.

Из логов nginx ежедневно собираются логи `monitoring`, куда сгружаются различные метрики с клиента, и `errors` — ошибки с клиента.

### SSH

Всегда можно зайти по ssh и что-нибудь погрепать. В кулауде машинки доступны магически по адресу (имя контейнера)-(номер контейнера).(имя контейнера).(имя окружения).(имя приложения).(имя проекта).stable.qloud-d.yandex.net. Например quinn-1.quinn.preproduction.webmail.mail.stable.qloud-d.yandex.net. Ну и можно посмотреть в интерфейсе кулауда, ткнув в `ISS` в плашке контейнера.

Nginx большой почты пока работает на железках, их много (можно посмотреть в executer'е `describe %mail_web`), корповый nginx в кулауде.

### Executer

Executer'ом можно запускать команды сразу на всей группе серверов — удобно погрепать самые свежие логи.

В конфиге заменить `username` на свой:

```(bash)
cat ~/.executer.conf
repo_user = username
default_user = username
shmux_threads = 15
shmux_timeout = 3000
exec_sort_byorder = 0
installer_args = -y -o "Dpkg::Options::":="--force-confnew"
project_filter = mail
```

Группы серверов в executer'е для кулауда формируются как название-проекта_название-приложения_название-окружения_название-контейнера.
Например mail_webmail_production_quinn, mail_verstka-qa_ub8_quinn. Командой `describe` можно посмотреть описание группы и все входящие в нее машинки:

```(bash)
[Serial] avanes> describe %mail_verstka-qa_ub8_quinn
  Group: mail_verstka-qa_ub8_quinn
  Project: mail
  Description: mail.verstka-qa.ub8.quinn
@sas
sas1-14b6103fa130.qloud-c.yandex.net
Total: 1
[Serial] avanes>
```

Nginx для production пока размещен на железных машинах, а не в кулауде, их группа называется `%mail_web`.

Для запуска команды на всей группе используй `p_exec`:

```(bash)
[Serial] username> p_exec %mail_webmail_production_quinn tail -100 /var/log/duffman/duffman-access.tskv | grep "HTTP_REQUEST_ERROR" | grep "sendbernar" || true
avanes@iva1-9d156d8aaa94.qloud-c.yandex.net: tskv   tskv_format=duffman-access-log  timestamp=2018-11-11 15:57:11   timezone=+0300  unixtime=1541941031 process_port=7103   duffman_wid=4   reason=HTTP_REQUEST_ERROR   url=sendbernar-qloud.mail.yandex.net:80/save_draft?caller=TOUCH&sc=&uid=609534885&v=1   method=POST error_type=RequestError message=Socket timed out on request to sendbernar-qloud.mail.yandex.net response_code=0 x_real_ip=94.41.6.55    x_request_id=2a4696677e5324e750cd3b4f966ba488   host=mail.yandex.ru project=TOUCH   handle=send-message uid=609534885
avanes@iva5-f3675d92d7a0.qloud-c.yandex.net: tskv   tskv_format=duffman-access-log  timestamp=2018-11-11 16:53:33   timezone=+0300  unixtime=1541944413 process_port=7102   duffman_wid=3   reason=HTTP_REQUEST_ERROR   url=sendbernar-qloud.mail.yandex.net:80/send_message?caller=TOUCH&sc=&uid=59951389&v=1  method=POST error_type=RequestError message=Socket timed out on request to sendbernar-qloud.mail.yandex.net response_code=0 x_real_ip=176.59.130.65 x_request_id=b736198d8fb6b3c06103ceaa59d50977   host=mail.yandex.ru project=TOUCH   handle=send-message uid=59951389
```
## YQL

Погрепать логи из YT можно с помощью [YQL](https://wiki.yandex-team.ru/yql/)

Для доступа к логам в idm нужно запросить роль YT-Hahn / mailfront.

Сферический пример:

```(yql)
PRAGMA yt.InferSchema;

SELECT * from hahn.[logs/mail-duffman-access-log/stream/5min/2018-11-11T12:10:00]
WHERE
    project='TOUCH' AND
    reason='REQUEST_FINISHED' AND
    status!='200'
;
```

[Пример с ошибками](https://yql.yandex-team.ru/Operations/WjEP78DhnD9Pe4JUOBDYXNWucwpkZYv39m6J3zOBL9Q=)

Полезный пример:

```(yql)
USE hahn;
SELECT error_type, msg, COUNT(login) AS c
FROM [//home/mailfront/errors-2017-09-10]
GROUP BY error_type, msg
ORDER BY c DESC;
```

[Пример с мониторингами](https://yql.yandex-team.ru/Operations/Wbvts3C-0qsVCzgLEQR79yYWx8pG_LlikXyxV35uf0A=)

Пример с ошибками рендера:

```(yql)
USE hahn;
$t = (SELECT request_dict{"message"} as msg, request_dict{"stack"} as stack
FROM [home/mailfront/errors-2019-02-14]
WHERE DictLookup(request_dict, "srv") = "touch" and DictLookup(request_dict, "version") = "6.0.36" and error_type = "render"
);

SELECT msg, stack, COUNT(*) AS total FROM $t GROUP BY msg, stack ORDER BY total DESC
```
