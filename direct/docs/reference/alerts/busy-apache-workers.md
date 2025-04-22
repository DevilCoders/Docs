# busy apache workers
_Это пока ещё не juggler-проверка, а только solomon—alert с уведомлением в чатик [{#T}](../chats.md#DISMonitoring)._


## Описание { #description }
Проверяем, что у нас не заканчиваются воркеры Apache (обслуживающие пользовательские запросы и alive—check'и балансера).  
Для этого сравниваем число занятых воркеров со значением настройки MaxClients.
Алерт не учитывает закрытость хоста от балансера.

Сравнивается сумма по всем хостам в ДЦ.
Значение MaxClients **захардкожено** в алерте (поэтому при изменении — нужно править и в алерте) и умножается на число метрик с данными.

## Диагностика { #diagnostics }
- Проверь: нет ли сейчас закрытых ДЦ, ожидаемо ли они закрыты (например на время регламентных работ)?
- Попробуй определить по графикам по trace—логов (ссылки ниже) — что тормозит или где привалило нагрузки

## Ссылки { #links }
* Конфигурация алертов в Solomon:
   * [busy apache workers: frontend / myt](https://solomon.yandex-team.ru/admin/projects/direct/alerts/apache_busy_workers_frontend_myt)
   * [busy apache workers: frontend / sas](https://solomon.yandex-team.ru/admin/projects/direct/alerts/apache_busy_workers_frontend_sas)
   * [busy apache workers: frontend / vla](https://solomon.yandex-team.ru/admin/projects/direct/alerts/apache_busy_workers_frontend_vla)
   * [busy apache workers: intapi / iva](https://solomon.yandex-team.ru/admin/projects/direct/alerts/apache_busy_workers_intapi_iva)
   * [busy apache workers: intapi / sas](https://solomon.yandex-team.ru/admin/projects/direct/alerts/apache_busy_workers_intapi_sas)
   * [busy apache workers: intapi / vla](https://solomon.yandex-team.ru/admin/projects/direct/alerts/apache_busy_workers_intapi_vla)
   * [busy apache workers: soap / iva](https://solomon.yandex-team.ru/admin/projects/direct/alerts/apache_busy_workers_soap_iva)
   * [busy apache workers: soap / sas](https://solomon.yandex-team.ru/admin/projects/direct/alerts/apache_busy_workers_soap_sas)
   * [busy apache workers: soap / vla](https://solomon.yandex-team.ru/admin/projects/direct/alerts/apache_busy_workers_soap_vla)
* Графики утилизации воркеров:
   * [frontend summary](https://solomon.yandex-team.ru/?project=direct&cluster=app_direct&service=perl-monitoring&apache=frontend&sensor=server_status_busy_workers&graph=auto&b=1h&e=&overLinesTransform=SUMMARY)
   * [intapi summary](https://solomon.yandex-team.ru/?project=direct&cluster=app_direct&service=perl-monitoring&sensor=server_status_busy_workers&graph=auto&b=1h&e=&overLinesTransform=SUMMARY&l.apache=intapi)
   * [soap summary](https://solomon.yandex-team.ru/?project=direct&cluster=app_direct&service=perl-monitoring&sensor=server_status_busy_workers&graph=auto&b=1h&e=&overLinesTransform=SUMMARY&l.apache=soap)
* Графики по trace—логам:
   * **web** [top 10 cmd ela](https://direct.yandex.ru/registered/main.pl?cmd=internalReports&sort=&reverse=&report_id=profile_logs_new&ir_param_time_period=4H&ir_param_stat_time_agg=5min&ir_param_filter_cmd_type=Cmd+PublicCmd+direct.perl.web&ir_param_filter_host_name=direct-perl-%25&ir_param_group_by_1=stat_time&ir_param_group_by_2=cmd&pivot_fields=cmd&pivot_measure=ela&show_chart=on&chart_type=area&chart_stacking=normal&chart_series_limit=10)
   * **web** [top 10 func ela](https://direct.yandex.ru/registered/main.pl?cmd=internalReports&report_id=profile_logs_new&ir_param_time_period=4H&ir_param_stat_time_agg=5min&ir_param_filter_cmd_type=Cmd+PublicCmd+direct.perl.web&ir_param_group_by_1=stat_time&ir_param_group_by_2=func&ir_param_group_by_3=func_param&ir_param_filter_host_name=direct-perl-%25&pivot_fields=func&pivot_fields=func_param&pivot_measure=func_ela&show_chart=on&chart_type=area&chart_stacking=normal&chart_series_limit=10)
   * **api** [top 10 cmd ela](https://direct.yandex.ru/registered/main.pl?cmd=internalReports&sort=&reverse=&report_id=profile_logs_new&xls=&ir_param_time_period=4H&ir_param_stat_time_agg=5min&ir_param_filter_cmd_type=direct.soap-api+direct.json-api+direct.xml-api+direct.api5&ir_param_filter_host_name=direct-perl-%25&ir_param_group_by_1=stat_time&ir_param_group_by_2=cmd&pivot_fields=cmd&pivot_measure=ela&show_chart=on&chart_type=area&chart_stacking=normal&chart_series_limit=10) 
   * **api** [top 10 func ela](https://direct.yandex.ru/registered/main.pl?cmd=internalReports&sort=&reverse=&report_id=profile_logs_new&ir_param_time_period=4H&ir_param_stat_time_agg=5min&ir_param_filter_cmd_type=direct.soap-api+direct.json-api+direct.xml-api+direct.api5&ir_param_filter_host_name=direct-perl-%25&ir_param_group_by_1=stat_time&ir_param_group_by_2=func&ir_param_group_by_3=func_param&pivot_fields=func&pivot_fields=func_param&pivot_measure=func_ela&show_chart=on&chart_type=area&chart_stacking=normal&chart_series_limit=10)
