## Src_setup
#### Что это?
Сервант аппхоста, через конфиг которого, можно завести прокси для источников, которые тяжело переводить на протокол аппхоста (либо если просто нужно быстро перевести сервис под аппхост, но часть источников не готова).
SRC_SETUP - платформа для написания аппхостовых сервантов.
#### Что может взорвать?
img/video
#### Когда обычно приезжает в очередь?
По будням в рабочие часы.
#### Когда обычно катим?
По будням в рабочие часы.
#### Сколько катится?
1,5ч
#### Как катать?

1. Найти тикеты вида `src_setup` в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases) и кликаем на любой:

   {% cut "Тикеты" %}

     ![1](_imgs/src1.png)

   {% endcut %}

1. Перейти в сервисы для каждой вертикали([imgs](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/app_host_imgs)/[video](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/app_host_video))

   {% cut "Выбор сервисов" %}

     ![2](_imgs/src2.png)

   {% endcut %}

1. Перейти в дашборд для каждой вертикали([imgs](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/app_host_imgs)/[video](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/app_host_video))

   {% cut "Переход в dashboard refs" %}

     ![3](_imgs/src3.png)

   {% endcut %}

1. Перейти в дашборд конкретной вертикали

   {% cut "Переход в дашборд" %}

     ![4](_imgs/src4.png)

   {% endcut %}

1. На странице дашборда добавить сортировку по itype 

   {% cut "Сортировка по itype" %}

     ![5](_imgs/src5.png)

   {% endcut %}

1. Скопировать номер тикета в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases)

   {% cut "Номер тикета" %}

     ![6](_imgs/src6.png)

   {% endcut %}

1. Отфильтровать по номеру тикета, начав с конца, погруппно коммитить

   {% cut "Фильтрация и порядок" %}

     ![7](_imgs/src7.png)

   {% endcut %}

1. Сначала select для группы с номером тикета, затем commit

   {% cut "Select&Commit" %}

     ![8](_imgs/src8.png)

   {% endcut %}

1. Подтвердить во всплывающем окне

   {% cut "Подтверждение" %}

     ![9](_imgs/src9.png)

   {% endcut %}

1. Повторить для каждой вертикали([imgs](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/app_host_imgs)/[video](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/app_host_video))

1. Обновить страничку в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases)

   {% cut "Обновление" %}

     ![10](_imgs/src10.png)

   {% endcut %}

1. Убедиться в смене статуса из "IN QUEUE" в статус "COMMITED" для всех значений

   {% cut "Смена статуса" %}

     ![11](_imgs/src11.png)

   {% endcut %}

1. Прожать deploy для каждой вертикали([imgs](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/app_host_imgs)/[video](https://nanny.yandex-team.ru/ui/#/services//dashboards/catalog/app_host_video))

   {% cut "Delpoy в dashboard" %}

     ![12](_imgs/src12.png)

   {% endcut %}

1. Выбрать рецепт `src_setup_ppsa_with_locks_queue` для всех вертикалей

   {% cut "Рецепт" %}

     ![13](_imgs/src13.png)

   {% endcut %}

1. Прожать deploy для каждой вертикали

   {% cut "Проверка и deploy" %}

     ![14](_imgs/src14.png)

   {% endcut %}

1. Проверить, что изменения коснулись только номеров id и подтвердить нажав deploy

   {% cut "Проверка diff'ов" %}

     ![15](_imgs/src15.png)

   {% endcut %}

#### Кого призывать при проблемах?
@elshiko в чате [SrcSetup Releases](https://t.me/joinchat/BwkfgA6-Mif5lJ7PnNCkpA)
#### Как откатывать?
Через [revert view](https://nanny.yandex-team.ru/ui/#/services/group_revert?serviceIds=hamster_app_host_man_pre_web_yp%2Chamster_app_host_man_web_yp%2Chamster_app_host_sas_web_yp%2Chamster_app_host_vla_web_yp%2Cprestable_app_host_sas_web_yp%2Cprestable_exp_app_host_sas_web_yp%2Cproduction_app_host_man_web_yp%2Cproduction_app_host_sas_web_yp%2Cproduction_app_host_vla_web_yp&recentSnapshotsCount=5).

