## Report
####  Что это?
Исторически report-ом называлась часть Поиска, написанная на perl и работающая в связке с Apache. Она принимала входящий запрос пользователя, проводила его минимальную предобработку, затем перенаправляла запрос в ReqWizard (Колдунщик запросов, ныне Begemot), а обогащённый колдунщиком запрос - в метапоиски. Ответ метапоиска передавался затем в шаблонизатор (templates) и отправлялся пользователю.
В настоящее время вся эта нетривиальная логика переехала в граф под apphost, часть логики предобработки - в http_adapter.
#### Что может взорвать?
Верхний метапоиск (upper, noapache).
#### Когда обычно приезжает в очередь?
В дневное время по будням, с примерной периодичностью 1 раз в месяц.
#### Когда обычно катим?
В дневное время по будням
#### Сколько катится?
1,5ч
#### Как катать?
В searchmon будет релиз с маской в названии: `report*report_core_package`.
Далее через дашборд [report](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/report) сделать commit тикетов, для deploy использовать рецепт `manual_confirmed_prepare_and_deploy_optimized_with_locks_queue`.
#### Кого призывать при проблемах?
Дежурных от [report](https://warden.yandex-team.ru/components/web/s/report).
#### Как откатывать?
Через [revert view](https://nanny.yandex-team.ru/ui/#/services/group_revert?serviceIds=production_report_man_web_yp%2Chamster_report_sas_web_yp%2Cproduction_report_vla_web_yp%2Chamster_report_vla_web_yp%2Cproduction_report_sas_web_yp%2Chamster_report_man_web_yp%2Cprestable_report_sas_web_yp&recentSnapshotsCount=5).
