## Введение
Прогрузка - регулярный процесс переливания трафика из нескольких ДЦ в один до тех пор, пока ему не станет плохо. Позволяет узнать реальный запас прочности сервиса, а также оперативно обноружить деградацию.
Таргет - зафиксированный RPS, который должен выдерживать один ДЦ. Если таргета не получилось достичь, то считаем, что это проблема, и надо с ней разбираться, даже в том случае, если на текущую нагрузку запаса хватает. Таргет пересматривается с изменением нагрузки, масштабированием железа и т.д.

## Таргет
- web:
  - java 580 rps ≈ 80% [vla](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-web&service=java-monitoring&l.sensor=jetty_requests&graph=auto&host=*.vla.yp-c.yandex.net&transform=differentiate&hideNoData=true&b=1h&e=) [sas](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-web&service=java-monitoring&l.sensor=jetty_requests&graph=auto&host=*.sas.yp-c.yandex.net&transform=differentiate&hideNoData=true&b=1h&e=) [iva](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-web&service=java-monitoring&l.sensor=jetty_requests&graph=auto&host=*.iva.yp-c.yandex.net&transform=differentiate&hideNoData=true&b=1h&e=)
  - perl 330 rps ≈ 75% [график*](https://solomon.yandex-team.ru/?project=direct&cluster=nginx-access&service=nginx-access&sensor=rps&response_code=ALL&host=Iva%7CSas%7CVla%7CMyt&graph=auto&l.vhost=direct.yandex.ru&b=1h&e=)
- api:
  - java 600 rps ≈80% [vla](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-api5&service=java-monitoring&l.sensor=jetty_responses_*&graph=auto&host=*.vla.yp-c.yandex.net&transform=differentiate&hideNoData=true&b=2h&e=) [sas](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-api5&service=java-monitoring&l.sensor=jetty_responses_*&graph=auto&host=*.sas.yp-c.yandex.net&transform=differentiate&hideNoData=true&b=2h&e=) [iva](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-api5&service=java-monitoring&l.sensor=jetty_responses_*&graph=auto&host=*.iva.yp-c.yandex.net&transform=differentiate&hideNoData=true&b=2h&e=)
  - perl 800 rps ≈85% [график*](https://solomon.yandex-team.ru/?project=direct&cluster=nginx-access&service=nginx-access&sensor=rps&response_code=ALL&host=Iva%7CSas%7CVla%7CMyt&graph=auto&l.vhost=api.direct.yandex.ru&b=1h&e=)
- intapi:
  - java 1100 rps ≈85% [vla](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-intapi&service=java-monitoring&l.sensor=jetty_responses_*&graph=auto&host=*.vla.yp-c.yandex.net&transform=differentiate&hideNoData=true&b=2h&e=) [sas](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-intapi&service=java-monitoring&l.sensor=jetty_responses_*&graph=auto&host=*.sas.yp-c.yandex.net&transform=differentiate&hideNoData=true&b=2h&e=) [iva](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-intapi&service=java-monitoring&l.sensor=jetty_responses_*&graph=auto&host=*.iva.yp-c.yandex.net&transform=differentiate&hideNoData=true&b=2h&e=)
  - perl 60 rps ≈100% =) [график*](https://solomon.yandex-team.ru/?project=direct&cluster=nginx-access&service=nginx-access&sensor=rps&response_code=ALL&host=Iva%7CSas%7CVla%7CMyt&graph=auto&l.vhost=intapi.direct.yandex.ru&b=1h&e=)
- uacfrontend:
    - nodejs 20 rps ≈100% [график](https://monitoring.yandex-team.ru/projects/direct/dashboards/monfu62erm9fkta44nk7/view/graph/dudpatxnl/queries?from=now-25m&to=now&refresh=60000) 

*надо учитывать, что часть трафика из графиков nginx дают запросы ручки alive:
 - web -≈70-80 rps/DC(с 9 балансеров на каждый из 10 хостов в дц)
 - api -≈200 rps/DC(с 9 балансеров на каждый из 10 хостов в дц)
 - intapi -≈30-40 rps/DC(с 9 балансеров на каждый из 5 хостов в дц)

## Процесс

1. История прогрузок доступна по [фильтру](https://st.yandex-team.ru/issues/?_f=type+priority+key+summary+description+status+resolution+created+updated+assignee+parent+rootCause&_q=Queue%3A+DIRECTADMIN+Tags%3A+%22type%3Atrainings%22+%22Sort+by%22%3A+Created+DESC))
2. Событие в Infra будет создано автоматически роботом. Если этого не произошло - запускаем событие через кнопку Add event слева в [интерфейсе](https://infra.yandex-team.ru). Заполняем в форме поля:
  - Service - Direct/Аварии и работы
  - Environment - prod
  - Data center - Прогружаемый(е) ДЦ
  - Type - Major maintenance
  - Title - Прогрузка <какой сервис>
  - Ticket - созданный в п.1 тикет
4. Наливаем в выбранный ДЦ трафик так, как описано в процессе прогрузки ниже. Меняем веса по [инструкции](./howto-dc-l7) После каждой итерации ждем примерно 5 минут, следим за таймингами и пятисотками
5. Если будет достигнут результат ощутимо больше таргета, то дальше идем по желанию. Если выполняется критерий остановки, сразу заканчиваем
6. Завершаем событие в Infra
7. Повторяем шаги выше по-очереди для перла и джавы.
8. Затем в заведенном таске фиксируем:
    - Приложение
    - Прогружаемый ДЦ
    - Достигнутый RPS и %
    - Причину остановки
    - Скриншоты графиков(rps, ошибок если были)
9. Записываем результаты(приложение/успешность/достигнутый таргет в perl/достигнутый таргет в java) в тикет DIRECTADMIN-9722 для агрегации

## Процесс прогрузки
Перед началом отключаем один ДЦ, чтобы имитировать отключение или учения
 - Начинаем с 50%(закрываем 1 ДЦ)
 - Каждые 2 минуты шагаем по 10% до 70%
 - Далее шагаем по 5%
 - Последние 2 шага делаем раз в 5 минут

## Мониторинги
Смотрим сразу в несколько мест:
- [Основной дашборд](https://solomon.yandex-team.ru/?project=direct&dashboard=direct-group-sre-tv&b=2h&e=)
- [Дашборд http-java](https://solomon.yandex-team.ru/?project=direct&dashboard=java-http-app&cluster=app_java-intapi%7Capp_java-web%7Capp_java-api5&b=2h&e=)
- [Тайминги работы гридов](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=common-metrics&l.monitoring_method=grid.api.*&l.sensor=traceLogTimeSpent&l.host=CLUSTER&l.monitoring_service=direct.web&l.env=production&graph=auto&filter=top&filterBy=avg&filterLimit=30&b=2h&e=)
- [График количества ошибок web](https://solomon.yandex-team.ru/?cluster=app_java-web&project=direct&service=java-monitoring&graph=message_log_errors&b=2h&e=&hideNoData=true)
- [Семафоры в web](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-web&service=java-monitoring&l.trace_interception_semaphore=*&l.env=production&l.sensor=used&graph=auto&b=1h&e=)
- [Тайминги ответов по балансерам](https://yasm.yandex-team.ru/panel/pe4kin._FJ6gwP/)
- [График 500к с балансера](https://solomon.yandex-team.ru/?project=direct&host=CLUSTER&service=awacs&graph=5xx_dashboard&b=2h&e=)
- [Алерты на CPU и память в Deploy](https://juggler.yandex-team.ru/raw_events/?project=direct.prod&query=host%3Dyasm_alert%26(service%3Ddirect.deploy-hw.prod.java-api5_cpu_limit_usage_perc%7Cservice%3Ddirect.deploy-hw.prod.java-web_cpu_limit_usage_perc%7Cservice%3Ddirect.deploy-hw.prod.java-intapi_cpu_limit_usage_perc%7Cservice%3Ddirect.deploy-hw.prod.java-api5_memory_limit_usage_perc%7Cservice%3Ddirect.deploy-hw.prod.java-web_memory_limit_usage_perc%7Cservice%3Ddirect.deploy-hw.prod.java-intapi_memory_limit_usage_perc))
- [Дашборд API](https://ppcgraphite.yandex.ru/grafana/dashboard/db/direct-api-monitoring?refresh=30s&orgId=1)
- [EB UAC](https://error.yandex-team.ru/projects/uac/projectDashboard?componentSettings=%7B%22row_1_col_0_con_0_charts%22%3A%7B%22scale%22%3A%22hour%22%2C%22autoRefresh%22%3Atrue%7D%7D&filter=savedFilter%20%3D%3D%20prod_nodejs_hot&period=hour)
- [EB Direct](https://error.yandex-team.ru/projects/direct?componentSettings=%7B%22row_1_col_0_con_0_charts%22%3A%7B%22autoRefresh%22%3Atrue%7D%7D&filter=environment%20%3D%3D%20production%20AND%20%28service%20%3D%3D%20direct.api5%20OR%20service%20%3D%3D%20direct.web%20OR%20service%20%3D%3D%20direct.intapi%29&period=hour)
- [Семафоры advq/метрики](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-web&service=java-monitoring&l.trace_interception_semaphore=*&l.env=production&l.sensor=used&graph=auto&b=1h&e=)
