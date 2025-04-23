## Upper (noapache)
#### Что это?
Верхний метапоиск development (upper, noapache). Исторически был получен методом отпиливания от apache report bundle метапоисковой части, и назвали его noapacheupper. С переходом на apphost было решено вернуться к имени upper. Работает в двухголовом режиме
* UPPER_INT (блок, опрашивающий источники под верхним метапоиском)
* BLENDER (переранжирования, в т.ч. блендер)
#### Что может взорвать?
Верхний метапоиск, следвательно сам поиск.
#### Когда обычно приезжает в очередь?
По будням, раз в день/раз в два дня.
#### Когда обычно катим?
В рабочее время по будням.
#### Сколько катится?
2-2,5ч
#### Как катать?

1. Находим три релиза, запоминаем номер релиза и проверяем наличие rearrange_dynamic в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases):

    * upper (noapacheupper_executable_red_id): upple/stable-*-*
    * upper (rearrange_data_res_id): upple/stable-*-*/arcadia/search/web/rearrs_upper
    * upper (noapache_rtcc_bundle_res_id): upple/stable-*-*

   {% cut "Номер релиза" %}

     ![1](_imgs/upper1.png)

   {% endcut %}

1. Кликаем на любой тикет

   {% cut "Разворот тикета" %}

     ![2](_imgs/upper2.png)

   {% endcut %}

1. Переходим в сервисы для каждой вертикали(web/img/video)

   {% cut "Выбор сервисов" %}

     ![3](_imgs/upper3.png)

   {% endcut %}

1. Переходим в дашборд сервисов для каждой вертикали:

   {% cut "Переход в дашборды" %}

     ![4](_imgs/upper4.png)

   {% endcut %}

1. Переход в дашборд конкретной вертикали: 
   * [web](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/noapache_web)
   * [imgs](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/noapache_imgs)
   * [video](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/noapache_video)

   {% cut "Переход в дашборд вертикали" %}

     ![5](_imgs/upper5.png)

   {% endcut %}

1. На странице дашборда добавить сортировку по itype

   {% cut "Сортировка по itype" %}

     ![6](_imgs/upper6.png)

   {% endcut %}

1. Начав с конца, погруппно коммитить **ВНИМАТЕЛЬНО ПРОВЕРЯЯ НОМЕР ТИКЕТА** в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases)

   {% cut "Commit с проверкой" %}

     ![7](_imgs/upper7.png)

   {% endcut %}

1. Подтверждать коммиты во всплывающем окне

   {% cut "Подтверждение коммитов" %}

     ![8](_imgs/upper8.png)

   {% endcut %}

1. Повторить для всех вертикалей(web/img/video) и **ВНИМАТЕЛЬНО ПРОВЕРИТЬ ПОЛНЫЙ ПЕРЕХОД ИЗ "IN QUEUE" В "COMMITED" ДЛЯ КАЖДОГО ТИКЕТА** в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases) и нажать deploy для каждой вертикали(web/img/video)

   {% cut "Проверка и deploy" %}

     ![9](_imgs/upper9.png)

   {% endcut %}

1. Проверить, что изменения коснулись только номеров id и подтвердить

   {% cut "Проверка diff'ов" %}

     ![10](_imgs/upper10.png)

   {% endcut %}

1. Выбрать рецепт и запустить deploy:
   * web `a1_with_locks_queue`
   * img `parallel_prepare_manual_deploy_with_locks_queue`
   * video `manualconfirm_deploy_prestable_with_locks_queue`

#### Кого призывать при проблемах?
Дежурных [upper](https://warden.z.yandex-team.ru/components/web/s/upper) в чате [DevOps Reactions (websearch)](https://t.me/joinchat/Qu9gEjzH9TfDPHH6) или в чате [Релизы и саппорт noapacheupper](https://t.me/joinchat/CaUODkNMIpwWNzLu4pngow). 
#### Как откатывать?
В каждом дашборде надо через revert view.
Сообщить дежурным сервиса что откатили.  

## Rearrange_dynamic
#### Что это?
Быстрые релизы формул и конфигурационных файлов верхнего метапоиска через rearrange.dynamic.
#### Что может взорвать?
Верхний метапоиск
#### Когда обычно приезжает в очередь?
По нескольку раз в сутки.
#### Когда обычно катим?
В рабочие часы по будням.
#### Сколько катится?
1,5
#### Как катать?
Так как катается теми же рецептами что и Upper (noapache), можно катать совместно с Upper (noapache). Но тогда труднее опредить что взорвалось.
#### Кого призывать при проблемах?
Аналогично Upper (noapache).
#### Как откатывать?
Аналогично Upper (noapache).

