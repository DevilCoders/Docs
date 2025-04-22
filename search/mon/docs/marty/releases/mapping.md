## Web graph mapping
#### Что это?
Внесение изменений в графы аппхоста.
#### Что может взорвать?
Источники аппхоста, следовательно взрывает только web
#### Когда обычно приезжает в очередь?
По будням в рабочее время. 2-3 раза в неделю.
#### Когда обычно катим?
По будням в рабочее время.
#### Сколько катится?
1,5ч
#### Как катать?
Выбираем в searchmon очереди релиз вида `web_graph_mapping (app_host_stable_branch)`. Далее проваливаемся в один из сервисов и оттуда в дашборд [app_host_web](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/app_host/)m накомичиваем тикеты, запускаем deploy с рецептом `app_host_ppsa_with_locks_queue`.

1. Находим релиз и запоминаем его номер в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases):

   {% cut "Найти и запомнить" %}

     ![1](_imgs/mapping1.png)

   {% endcut %}

1. Раскрыть релиз и пройти в сервис

   {% cut "Сервис" %}

     ![2](_imgs/mapping2.png)

   {% endcut %}

1. Провалиться в дашборд [app_host_web](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/app_host)

   {% cut "Dashboard" %}

     ![3](_imgs/mapping3.png)

   {% endcut %}

1. Активировать сортировку по itype

   {% cut "Сортировка по itype" %}

     ![4](_imgs/mapping4.png)

   {% endcut %}

1. Начав с конца, погруппно коммитить **ВНИМАТЕЛЬНО ПРОВЕРЯЯ НОМЕР ТИКЕТА** в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases) 

   {% cut "Commit с проверкой" %}

     ![5](_imgs/mapping5.png)

   {% endcut %}

1. Подтверждать коммиты во всплывающем окне

   {% cut "Подтверждение коммитов" %}

     ![6](_imgs/mapping6.png)

   {% endcut %}

1. **ВНИМАТЕЛЬНО ПРОВЕРИТЬ ПОЛНЫЙ ПЕРЕХОД ИЗ "IN QUEUE" В "COMMITED" ДЛЯ КАЖДОГО ТИКЕТА** в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases)

   {% cut "Проверка в SEARCHMON" %}

     ![7](_imgs/mapping7.png)

   {% endcut %}

1. Выбираем deploy в [DASHBOARD](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/app_host)

   {% cut "Deploy" %}

     ![8](_imgs/mapping8.png)

   {% endcut %}

1. Выбираем рецепт app_host_ppas_with_locks_queue

   {% cut "Рецепт app_host_ppas_with_locks_queue" %}

     ![9](_imgs/mapping9.png)

   {% endcut %}

#### Кого призывать при проблемах?
Автора релиза (из описания релизного тикета) в чате [WEB Report, Graphs & RequestInit Releases](https://t.me/joinchat/CaUODkYSN2MyE5jE9xgJzg). Так как в warden компонента не занесена, можно найти дежурного [тут](https://rm.z.yandex-team.ru/component/web_graph_mapping) в графе `Responsible`. Обычно это @alex-ersh, @avitella, @feldsherov, @elshiko.
#### Как откатывать?
Через [revert view](https://nanny.yandex-team.ru/ui/#/services/group_revert?serviceIds=hamster_app_host_man_web_yp,production_src_setup_man_web_yp,prestable_app_host_sas_web_yp,hamster_app_host_man_pre_web_yp,production_app_host_man_web_yp,hamster_app_host_sas_web_yp,prestable_exp_app_host_sas_web_yp,hamster_src_setup_man_web_yp,production_src_setup_sas_web_yp,hamster_src_setup_vla_web_yp,production_app_host_sas_web_yp,production_app_host_vla_web_yp,hamster_src_setup_sas_web_yp,prestable_src_setup_sas_web_yp,production_src_setup_vla_web_yp,hamster_app_host_vla_web_yp&recentSnapshotsCount=5).

