## Begemot
#### Что это?
Сервис, который преобразует исходный запрос пользователя в формат, понятный поисковому рантайму (разбор запроса, обогащение синонимами, представление в виде qtree/reqbundle), считает запросные факторы, классифицирует запрос.
#### Что может взорвать?
Используется в вебе, видео, картинках, Алисе, геопоиске, а также поиске музыки, маркета, этушки и всяких других.
Катить в прайм-тайм нельзя, т.к. размывает кеш на средних.
#### Когда обычно приезжает в очередь?
Вечером, после 22:00 по будням
####  Когда обычно катим?
После 23:00 по будням перед выкаткой баз поискового индекса.
#### Сколько катится?
3ч.
#### Как катать?

1. На главной странице [Nanny](https://nanny.yandex-team.ru/ui/#/) перейти в [dashboards](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog):

   {% cut "Переход в dashboards" %}

     ![1](_imgs/Begemot1.png)

   {% endcut %}

1. Отфильтровать на странице по begemot и перейти в [Begemot Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/begemot)(begemot & wizard)

   {% cut "Переход в Begemot Dashboard" %}

     ![2](_imgs/Begemot2.png)

   {% endcut %}

1. Проверить появление новой закомиченной версии

   {% cut "Проверка наличия релиза" %}

     ![3](_imgs/Begemot3.png)

   {% endcut %}

1. Перейти в deploy

   {% cut "Переход в deploy" %}

     ![4](_imgs/Begemot4.png)

   {% endcut %}

1. Если катим утром: выбрать утренний рецепт deploy 

   {% cut "Утренний рецепт deploy" %}

     ![5](_imgs/Begemot6.png)

   {% endcut %}

1. Если катим вечером(начинать в ~22:30): выбрать вечерний рецепт: deploy_day_fast

   {% cut "Вечерний рецепт: deploy_day_fast" %}

     ![6](_imgs/Begemot5.png)

   {% endcut %}

1. На странице рецепта перейти в deploy

   {% cut "Deploy" %}

     ![7](_imgs/Begemot7.png)

   {% endcut %}

1. Внимательно ознакомиться с diff(при обнаружении серьезных изменений спросить у команды begemot) и подтвердить

   {% cut "Проверка diff и подтверждение diff" %}

     ![8](_imgs/Begemot8.png)

   {% endcut %}

1. Preparing-кубы не требуют подтверждения

   {% cut "Подтверждение кубов" %}

     ![9](_imgs/Begemot9.png)

   {% endcut %}

#### Кого призывать при проблемах?
[gluk47@](https://staff.yandex-team.ru/gluk47), если не удается связаться то дежурные от [begemot](https://warden.yandex-team.ru/components/begemot). Чат [begemoting](https://t.me/joinchat/B5EDfEDnX06iR6GTsfKrEw). При проблемах необходимо сделать SPI $
#### Как откатывать?
Через дежурных от [begemot](https://warden.yandex-team.ru/components/begemot).
