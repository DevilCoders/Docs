## Флаги
#### Что это?
Прошедшие проверку эксперименты, теперь уже на всех пользователей
#### Что может взорвать?
Взорвать могут также все, но катятся полокационно.
#### Когда обычно приезжает в очередь?
по будням в рабочее время
#### Когда обычно катим?
по будням в рабочее время
#### Сколько катится?
1,5ч
#### Как катать?
Проваливаемся в любой сервис, затем в дашборд [report_data_all](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/report_data_all), накомичиваем тикеты нужного релиза, далее deploy, рецепт new_shiny_flags_deploy_with_locks.
1. Найти тикет вида `SEAREL-*: Update flags.json to the version * [web]` в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases):

   {% cut "Тикеты" %}

     ![1](_imgs/flags1.png)

   {% endcut %}

1. Перейти в любой сервис

   {% cut "Выбор сервисов" %}

     ![2](_imgs/flags2.png)

   {% endcut %}

1. Перейти в Dashboards Refs

   {% cut "Переход в dashboard refs" %}

     ![3](_imgs/flags3.png)

   {% endcut %}

1. Перейти в дашборд report_data_all

   {% cut "report_data_all" %}

     ![4](_imgs/flags4.png)

   {% endcut %}

1. На странице дашборда добавить сортировку по itype 

   {% cut "Сортировка по itype" %}

     ![5](_imgs/flags5.png)

   {% endcut %}

1. Скопировать номер тикета в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases)

   {% cut "Номер тикета" %}

     ![6](_imgs/flags6.png)

   {% endcut %}

1. Отфильтровать по номеру тикета и пролистать в конец

   {% cut "Фильтрация и порядок" %}

     ![7](_imgs/flags7.png)

   {% endcut %}

1. Сначала select для группы с номером тикета, затем commit

   {% cut "Select&Commit" %}

     ![8](_imgs/flags8.png)

   {% endcut %}

1. Подтвердить во всплывающем окне

   {% cut "Подтверждение" %}

     ![9](_imgs/flags9.png)

   {% endcut %}

1. Обновить страничку в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases)

   {% cut "Обновление" %}

     ![10](_imgs/flags10.png)

   {% endcut %}

1. Убедиться в смене статуса из "IN QUEUE" в статус "COMMITED" для всех значений

   {% cut "Смена статуса" %}

     ![11](_imgs/flags11.png)

   {% endcut %}

1. Прожать deploy

   {% cut "Delpoy в dashboard" %}

     ![12](_imgs/flags12.png)

   {% endcut %}

1. Выбрать рецепт `new_shiny_flags_deploy_with_locks_queue`

   {% cut "new_shiny_flags_deploy_with_locks_queue" %}

     ![13](_imgs/flags13.png)

   {% endcut %}

1. Прожать deploy

   {% cut "deploy" %}

     ![14](_imgs/flags14.png)

   {% endcut %}

1. Проверить, что изменения коснулись только номеров id и подтвердить, нажав deploy

   {% cut "Проверка diff'ов" %}

     ![15](_imgs/flags15.png)

   {% endcut %}
#### Кого призывать при проблемах?
Чат [выкатка на 100%](https://t.me/joinchat/Tqp1-86s8c9_Bz7f). @buryakov + @assenova + дежурный от [ab/uaas](https://warden.z.yandex-team.ru/components/ab/s/uaas).
#### Как откатывать?
Через [revert view](https://nanny.yandex-team.ru/ui/#/services/group_revert?serviceIds=hamster_flags_provider_man_web_yp%2Chamster_flags_provider_sas_web_yp%2Chamster_flags_provider_vla_web_yp%2Cprestable_flags_provider_sas_web_yp%2Cproduction_flags_provider_man_web_yp%2Cproduction_flags_provider_sas_web_yp%2Cproduction_flags_provider_vla_web_yp&recentSnapshotsCount=5).
