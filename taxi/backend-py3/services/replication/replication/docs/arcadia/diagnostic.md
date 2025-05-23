## Проверка работы с источником { #source_validation }
Перед тем как добавить новый источник, стоит проверить, что репликация может подключиться
к источнику и получить всю необходимую для работы репликации информацию.
[Подробная инструкция по шагам](source_validation.md)

## Тестирование

1. Первым этапом нужно убедиться, что ваши правила появились в админке {{ description_replication_admin }}.
2. После этого, перейдя в вашу группу правил, напротив таргетов, кроме api-источников, можно найти ссылки
**replication cron**. У ext-target'ов ссылка будет вести на логи в Кибане. Для остальных таргетов откроется
список запусков кронов. Каждый крон имеет один из 3-х статусов: **выполнение**, **завершён** и **ошибка**.
3. Также напротив каждого таргета есть ещё одна очень полезная ссылка **grafana target graphs**. Перейдя
по ней, вы сможете следить:

      * за **отставаниями репликации**:
           * **base delay from now** показывает отставание репликации относительно текущего времени
             (если это значение растёт и не убывает, то вероятно что-то сломалось);
           * **sync delay from now** показывает отставание между синками батчей при заливке (считается
             нормально, когда это значение не более 10-ти минут; если значение достигает нескольких часов,
             то значит что-то сломалось); название этих параметров совпадает с названием соответствующих графиков,
             графики находятся во вкладках с названием правила и с названием таргета;
      * за количеством **документов в очереди** (это значение можно найти как **total docs** на графике **number
        of docs in queue** на вкладке с названием правила);
      * за количеством **неотреплицированных документов в очереди** (это значение можно найти как **unreplicated
        docs** на графике **number of docs in queue** на вкладке с названием правила);

4. Отставание должно периодически сокращаться и не должно резко расти. Количество неотреплицированных
документов  должно периодически уменьшаться (это значит, что таргеты вычитывают документы из очереди) и
периодически расти (значит источник что-то пишет в очередь). При этом репликация не удаляет документы из
очереди - это делает архивация очередей, которая запускается по своему расписанию независимо от репликации.
У каждого правила есть соответсвующий крон архивации очереди, его название формируется по шаблону
**replication-archive-queue_mongo-{*имя правила*}**. [Вот](https://tariff-editor.taxi.yandex-team.ru/dev/cron?service=replication&name=archive)
список кронов архивации очередей.
5. Если нажать на таргет, у которого тип таргета YT, то в открывшемся поле можно найти *yt_path* - путь в YT,
перейдя по которому можно посмотреть на отреплицированные данные.

## Локальная репликация
В некоторых случаях, если вы постоянно добавляете новые правила и не хотите тратить время на их деплой в тестинг и включение в админке,
есть возможность настроить локальную репликацию. [Инструкция на вики](https://wiki.yandex-team.ru/users/desire/remotepycharm).

## Графики очередей

Существуют графики, на которых можно следить за состоянием очередей. Для каждой очереди рисуется три дашборда:

1. На верхнем и самом широком можно следить за размером очереди, за количеством доступного места, а также за квотой,
   которая считается как сумма всех квот правил, реплицирующих документы через эту очередь.

2. На втором ряду слева можно увидеть графики с ошибками, которые возникали на этом кластере.

3. На втором ряду справа расположились графики "размеров правил": сколько места занимают все документы, реплицируемые
   каждым правилом через эту очередь.

Ссылки на графики: [прод]({{ link_to_taxi_replication_queue_mongo_stat }}), [тестинг]({{ link_to_taxi_replication_queue_mongo_stat_testing }}).

## Как следить за релизом правил и сервиса (разработчикам сервиса)

* Общие [логи в кибане]({{ link_to_kibana_sevice_logs }}).
* [Графики web]({{ link_to_dashboard_nanny_taxi_replication }})
* [Логи web в кибане]({{ link_to_kibana_replication_web_logs }})
* [Графики cron]({{ link_to_dashboard_nanny_taxi_replication-tasks }})
* [Логи cron в кибане]({{ link_to_kibana_replication_tasks_logs }})
* Графики по правилам, ссылки по таргетам есть и в админке,
но тут также интересна самая верхняя панель,
с информацией по очередям:
    * **testing**: [{{ link_to_testing_dashboards }}]({{ link_to_testing_dashboards }})
    * **production**: [{{ link_to_dashboards }}]({{ link_to_dashboards }})

## Где смотреть логи, если в кибане их уже нет
Логи репликации доставляются через logbroker в таблички yt и хранятся там по дням.
* [Логи для веба репликации]({{ link_web_logs_to_yt_table }})
* [Логи для крон репликации]({{ link_tasks_logs_to_yt_table }})
