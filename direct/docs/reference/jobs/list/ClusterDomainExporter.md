## ClusterDomainExporter

### Продукт/подсистема

Агентские комиссии, деньги.


### Роль в работе продукта/подсистемы

Выгружает справочник "кластерных" доменов в YT.

Существуют интернет-ресурсы, в которых их пользователи могут создавать собственные странички и рекламировать их в Директе. Например, страницы в Instagram или ВКонтакте. Ссылки на такие сервисы Директ преобразовывает таким образом, чтобы у разных пользователей на одном домене получались собственные отличные друг от друга домены. Например, `instagram.com/vasya` -> `vasya.instagram.com`.

Такие преобразованные домены, а точнее, хэш от них, оседают в логах БК. Биллинг, в свою очередь, расчитывает агентские комиссии, и для этого ему нужно связать логи БК с доменами клиента. Для этой цели данная джоба создаёт в YT словарь, в котором присутствует преобразованный домен, часть урла, из которой он сформирован, и его хэш (`Yabs::BobHash`).


### Датафлоу

Первоисточник данных о преобразованных доменах - таблица [ppc.aggregator_domains](https://direct-dev.yandex-team.ru/db/ppc/tables/aggregator_domains.html). Она выгружается в YT в выгрузку для аналитиков, которую поддерживает Директ (другой джобой) в таблицу [//home/direct/db/aggregator_domains](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/db/aggregator_domains).

Что делает сама джоба:
- Собирает уникальные строки (поле `pseudo_domain`) из таблицы [//home/direct/db/aggregator_domains](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/db/aggregator_domains).
- Накладывает на них функцию [Yabs::BobHash](https://yql.yandex-team.ru/Operations/XIZNCTa9vOQXQVKPOAhLtMKTaA04qdGZTcfpyiUFTxw=).
- Обновляет данные в [//home/direct/dict/ClusterDomain](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/dict/ClusterDomain) (на Hahn/Arnold).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ClusterDomainExporter.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'export.ClusterDomainExporter)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Из-за того что справочник в YT по таким доменам станет не актуальным, часть комиссий может посчитаться не корректно - это критично.


### Как пользователи (или команда) заметят проблему и через какое время

Агентства или менеджеры, отвечающие за премии, могут заметить неверные комиссии.


### Контакты разработчиков и менеджеров

Разработчики: [Алексей Кашицын](https://staff.yandex-team.ru/aliho)


### Желательное время исправления в случае поломки

День.


### Способы регулирования работы джобы

-


### Известные причины поломок

-


### Дополнительно: тонкости и подводные камни

Есть тикет по выпиливанию всего этого в пользу DWH: https://st.yandex-team.ru/DIRECT-130070
