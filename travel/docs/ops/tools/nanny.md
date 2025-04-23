---
title: Няня (Nanny)
---

## Общая документация

Находится в [Wiki](https://wiki.yandex-team.ru/runtime-cloud/nanny/)

## Сборник HOWTO

### Как откатить релиз

Всё сломалось, и надо срочно откатить? Инструкция ниже.

#### Откат на предыдущую версию

1. Заходим в сервис, например [Orders Testing](https://nanny.yandex-team.ru/ui/#/services/catalog/travel_orders_app_testing/)

2. На активном снепшоте нажимаем Rollback

3. Убеждаемся, что в Description написан нужная версия сервиса.

4. Убеждаемся, что поставлена галочка `Set rollback snapshot as current`

5. Жмём `Apply`
  ![Скрин](https://jing.yandex-team.ru/files/alexcrush/nanny1-1.png)

#### Откат на более старую версию

1. Заходим в сервис, например [Orders Testing](https://nanny.yandex-team.ru/ui/#/services/catalog/travel_orders_app_testing/)

2. Выбираем снэпшот, на который хотим откатить. обычно это предыдущий снэпшот.
   Нажимаем у этого снэпшота `Change`
   ![Скрин](https://jing.yandex-team.ru/files/alexcrush/nanny2.png)

3. В открывшемся окне нажимаем `Active` и **обязательно** ставим галочку `Set snapshot as current`
   ![Скрин](https://jing.yandex-team.ru/files/alexcrush/nanny3.png)

4. Нажимаем `Apply`

Чтобы не забывать ставить галочку `Set snapshot as current` можно в настройках сервиса (`Information` -> `General`) выставить настройку `Set snapshot as current upon activation` в `True`

Чтобы откатить откат, проделываем те же манипуляции, нажимая `Change` у нужного снепшота.
