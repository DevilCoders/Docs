Мониторинги
===========
Расчёт заработной платы сдельным сотрудникам базируется на информации поставляемой рядом источников. Данные поставки могут быть нестабильными. Для предотвращения неправильного расчёта в случае проблем с источником данных существуют следующие мониторинги:
- мониторинг копирования данных из PostgreSQL таблиц Народной Карты в YT; и
- мониторинг копирования данных из Трекера в YT.


Что делать если зажёгся мониторинг?
-----------------------------------
Если в момент расчёта заработной платы необходимые данные ещё не скопированы в YT, то лучшим решением является приостановка расчёта в Нирване ([/home/robot-wikimap/Tasks Payment/Tasks Payment][tasks-payment-reaction]) с последующим его перезапуском после нормализации ситуации с поставками данных. Это связанно с тем, что в противном случае перед повторным расчётом также потребуется удаление уже посчитанных данных из [отчёта][report], что является нетривиальной деструктивной задачей.

Так как расчёт стартует в три часа начи, то и проблемы с поставками данных являются критичными только в ночное время.

Если мониторинг зажёгся в ночное время до трёх часов ночи, то дежурный должен поставить расчёт на паузу. Мониторинг зажёгшийся после трёх часов ночи можно проигнорировать до утра.

Все последствия должны обрабатываться в штатном порядке в нормальное рабочее время.


Мониторинг копирования данных из PostgreSQL в YT
------------------------------------------------
Данный мониторинг следит за свежестью данных в YT которые туда копируются из Народной картой с помощью [Трансфер менеджера][tm]. Информация о его активности сохраняется в Соломоне и доступна на [дешборде][solomon-tm-replication-dashboard]. В свою очередь, в Народных Картах используется [Джаглер][juggler]. Для объединения этих двух систем, в Соломоне настроен [алерт PostgreSQL to YT Replication Delay (Social)][solomon-psql-to-yt]. Этот алерт пробрасывается в мониторинг настроенный в Джаглере: [`host=solomon-alert, service=nmaps_dynamic_replica_social`][juggler-psql-to-yt].


Мониторинг копирования данных Трекера в YT
------------------------------------------
Данный мониторинг следит за состоянием сервиса обеспечивающего копирование данных из Трекера в YT. За этот сервис отвечает команда Трекера. Он запускается раз в полчаса и за его состоянием можно следить с помощью [соответсвующего мониторинга][juggler-base-tracker-to-yt]. Однако данный мониторинг может поджечься даже в случае нефатального для расчёта заработной платы отставания. Для увеличения времени необходимого для срабатывания мониторинга (а также настройки оповещений) события используемые в мониторинге выше объединены с помощью флаподава в более длинные события: [`host=tracker, service=sync_to_yt`][juggler-tracker-to-yt].


[juggler-base-tracker-to-yt]: https://juggler.yandex-team.ru/check_details/?host=deploy.startrek-api-production.startrek-backend-bazinga&service=http_check_monitoring_yTSyncTablesStatus
[juggler-psql-to-yt]: https://juggler.yandex-team.ru/check_details/?host=solomon-alert&service=nmaps_dynamic_replica_social
[juggler-tracker-to-yt]: https://juggler.yandex-team.ru/check_details/?host=tracker&service=sync_to_yt
[juggler]: https://juggler.yandex-team.ru
[report]: https://stat.yandex-team.ru/Maps.Wiki/tasks_payment/Tasks_Payment
[solomon-psql-to-yt]: https://solomon.yandex-team.ru/admin/projects/maps-nmaps/alerts/16229798-f32e-4d15-9cef-b7221ecac99b
[solomon-tm-replication-dashboard]: https://solomon.yandex-team.ru/?project=data-transfer&cluster=rtc-prod&dashboard=transfer_dashboard&l.resource_id=*dttaf8uilqb0kmt3wyhl&l.source_type=pg&l.target_type=yt&l.source_id=mdb6od92oiks2maqel86&l.target_id=hahn--home-maps-nmaps-dynamic-replica-social&b=1h
[tasks-payment-reaction]: https://beta.nirvana.yandex-team.ru/browse?selected=4711127
[tm]: https://wiki.yandex-team.ru/transfer-manager/replication
