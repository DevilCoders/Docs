## Словари
#### Что это?
Словари SDCH для графов в аппхосте  
#### Что может взорвать?
WEB-поиск  
#### Когда обычно приезжает в очередь?
В выходные
#### Когда обычно катим?
В воскресенье днем.([ПРИМЕР](https://calendar.yandex-team.ru/event/52116743)  
#### Сколько катится?
Каждая  фаза 20-30 минут  
#### Как катать?
1. Развернуть 1-ую фазу в очереди [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases)

   {% cut "Разворот фазы" %}

     ![1](_imgs/SDCH1.png)

   {% endcut %}

1. Выбрать любой сервис в 1-ой фазе

   {% cut "Выбор сервиса" %}

     ![2](_imgs/SDCH2.png)

   {% endcut %}

1. Выбрать Dashboards Refs на странице сервиса

   {% cut "Dashboard Refs" %}

     ![3](_imgs/SDCH3.png)

   {% endcut %}

1. Выбрать sdch encoders dashboard

   {% cut "sdch encoders dashboard" %}

     ![4](_imgs/SDCH4.png)

   {% endcut %}

1. **ТОЛЬКО ДЛЯ ОДНОЙ ФАЗЫ В ПОРЯДКЕ ОЧЕРЕДИ** Select & Commit 

   {% cut "Select&Commit" %}

     ![5](_imgs/SDCH5.png)

   {% endcut %}

1. Только убедившись в коммитах **ОДНОЙ ИЗ ФАЗ В ПОРЯДКЕ ОЧЕРЕДИ** в [SEARCHMON](https://nanny.yandex-team.ru/ui/#/queues/meta/SEARCHMON/releases) - нажать Deploy

   {% cut "Deploy" %}

     ![6](_imgs/SDCH6.png)

   {% endcut %}

1. Выбрать рецепт из выпадающего списка: default

   {% cut "Рецепт default" %}

     ![7](_imgs/SDCH7.png)

   {% endcut %}

1. Проверить, что изменения коснулись только номеров id

   {% cut "Проверка diff'ов" %}

     ![8](_imgs/SDCH8.png)

   {% endcut %}

Только при полном окончании 1-ой фазы, переходим к следующей, по порядковому номеру фазы. 
#### Кого призывать при проблемах?
@feldsherov
#### Как откатывать?
При необходимости воспользоваться [revert view](https://nanny.yandex-team.ru/ui/#/services/group_revert?serviceIds=man_sdch_encoder_yp%2Csas_sdch_encoder_yp%2Cvla_sdch_encoder_yp&recentSnapshotsCount=5).
Откатывать следует к состоянию до накатки фазы 1 текущего нового релиза (формально к фазе 3 старого релиза).
