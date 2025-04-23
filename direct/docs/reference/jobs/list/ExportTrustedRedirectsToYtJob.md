# ExportTrustedRedirectsToYtJob


### Продукт/подсистема

Экспорт в Бк данных о доменах счетчиков.


### Роль в работе продукта/подсистемы

Сервис Баннерная Крутилка(БК) умеет проверять, что определенный домен работает. Это необходимо для того, чтобы остановить показ рекламы неработающего сайта.
В БК сделан мониторинг с этой проверкой: [wiki](https://wiki.yandex-team.ru/bannernajakrutilka/urlmonitoring2/).

Директ же умеет говорить БК, что некоторые домены, например: rdr.salesdoubler.com.ua, yadcounter.ru -- мониторить не нужно, это счетчики -- специальные сайты, которые собирают статистику по переходам из директовых баннеров, а затем через редирект отправляют на нужный домен. 
Данные о доменах счетчиков находятся в: [ppcdict.trusted_redirects](https://direct-dev.yandex-team.ru/db/ppcdict/tables/trusted_redirects.html).

Джоба умеет экспортировать такие домены для БК.

Меняются через ручку:
- [интерфейс](https://direct.yandex.ru/registered/main.I9g-uKlcsTV71ieE.pl?cmd=trustedRedirects)
- [код](https://a.yandex-team.ru/arc/trunk/arcadia/direct/web/src/main/java/ru/yandex/direct/web/entity/internaltools/controller/TrustedRedirectsController.java#L46)
- [ppc_log_cmd](https://direct.yandex.ru/logviewer/#~(logType~'ppclog_cmd~form~(from~'20200406T000000~to~'20210406T235959~fields~(~'log_time~'uid~'role~'cluid~'cid~'service~'cmd~'runtime~'param~'http_status~'response~'ip~'reqid~'trace_id)~conditions~(reqid~'4134639364093069804)~limit~1000~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
- [binlog](https://direct.yandex.ru/logviewer/#~(logType~'binlog_rows_v2~form~(from~'20200406T000000~to~'20210406T235959~fields~(~'datetime~'source~'table~'service~'method~'primary_key~'operation~'row~'reqid)~conditions~(table~'trusted_redirects)~limit~1000~offset~0~reverseOrder~false~showTraceIdRelated~false))$)

Обычно пользователи запрашивают добавление их счетчика: [wiki](https://wiki.yandex-team.ru/accountdirect/counter/#dobavlenieschetchikavnashubazu).


### Датафлоу

1) Удаляем все данные из [markov.//home/direct/export/trusted_domain](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/direct/export/trusted_domain).
2) Затем сохраняем записи из [ppcdict.trusted_redirects](https://direct-dev.yandex-team.ru/db/ppcdict/tables/trusted_redirects.html), у которых redirect_type == counter в [markov.//home/direct/export/trusted_domain](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/direct/export/trusted_domain).

Джоба запускается раз в день.


### Какая функциональность пострадает от отказа джобы

Мониторинг БК какое-то время будет простукивать лишние хосты.


### Как пользователи (или команда) заметят проблему и через какое время
Кажется, что пользователь не знает о существовании мониторингов, и не сможет понять никак, что джоба отвалилась. 
Мониторинг БК обстукивает домены, не урлы (таблица состояний доменов: [markov.//home/yabs/url_monitoring/states](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/yabs/url_monitoring/states)). 

Поэтому счетчики не станут искажать данные о переходах, и это не вызвовет проблем у клиента.

Команде не заметить.


### Контакты разработчиков и менеджеров

Эти герои остались в легендах.


### Желательное время исправления в случае поломки

Неделя+.


### Способы регулирования работы джобы

В проперте `export_trusted_redirects_last_execution` хранится день последнего запуска джобы, для запуска он не должен совпадать с текущим.


### Известные причины поломок

