# Интерация rest-menu-storage и restaurant-menu

## Проблема
Сейчас меню ресторано отдается из коры, хотим перевести перевести его на
новый сервис eats-rest-menu-storage.

## Как работает сейчас

![now](./img/now.png)

<!--
@startuml img/now.png

"api-proxy" -> "eda_core": Запрос за меню (с фронта)
"api-proxy" <- "eda_core": Меню ресторана
"api-proxy" -> "eats-restaurant-menu": Меню ресторана
"api-proxy" <- "eats-restaurant-menu": Модифицированное меню

@enduml
-->

Запрос с фронта попадает в api-proxy, которая делает запорос в кору,
результат из коры отправляет в restaurant-menu, который его модифицирует
и возвращает обратно в api-proxy.

## Как хотим

Первым этапом задача сводится к тому, чтобы просто заменить источник данных
с коры на rest-menu-storage, без логики вычисления динамических категорий.

### Задачи
#### rest-menu-storage
1) Отправлять КБЖУ из коры в rest-menu-storage
2) Сохранять КБЖУ на стороне rest-menu-storage
3) Отдавать КБЖУ в клиентских ручках rest-menu-storage

#### restaurant-menu
1) Написать ручку, аналогичную по [спеке](https://bb.yandex-team.ru/projects/EDA/repos/spec-api/browse/specs/client_core_v2/spec.yml#69) ручке в коре. Под капотом, ручка
будет делать запрос в кору, а после модифицировать так же как сервис делал до этого.
2) Написать код, который под экспериментом помимо коры ходит и в rest-menu-storage.
Нужно предусмотреть несколько вариантов работы
- только запрос и сравнение результатов (расхождение писать в лог)
- отдача статичесих категорий и айтемов в них из rest-menu-storage
При этом в последнем варианте, для динамических категорий
модель айтема тоже нужно брать из rest-menu-storage, из ответа коры использовать только
множество id айтемов в ней.
3) Написать правила api-proxy, которые перенаправляют трафик со старой схемы на новую

Опредееление доступности айтемов по стокам и расписанию категорий
уже реализована в rest-menu-storage, но на стороне клиентского меню нужно
- исключать айтемы в стоплистах для лавки и аптек
- добавлять picture_scale на основе информации о бренде (в restaurant-menu уже есть кэш каталога и эта информация)
- формировать КБЖУ-строку так же как это делается в коре

#### eats-cart

Есть информация про при переключении меню ретейла и рассинхронизации данных в меню и корзине были проблемы,
поэтому переключение на использование данных из rest-menu-storage, нужно сделать аналогичное переключение
и в сервисе eats-cart.
Сейчас корзина ходит в ручку get-items, в rest-menu-storage есть аналогичная ручка с похожим API.


#### eats-upsell

Код по переезду с коры на rest-menu-storage уже написан в рамках https://st.yandex-team.ru/EDACAT-2679
Эксперимент в тестинге: https://tariff-editor.taxi.tst.yandex-team.ru/experiments3/experiments/show/eats_upsell_use_rest_menu_storage/current?active=all&enabled=all&is_technical=all&name=eats_upsell_use_rest_menu_storage


#### Переезд на eats-discounts

Должен случиться в мае силами команды Jam.


Целевая схема в рамках этого этапа выглядит так:

![now](./img/new.png)

<!--
@startuml img/new.png

"api-proxy" -> "eats-restaurant-menu": Запрос за меню (с фронта)
"eats-restaurant-menu" -> "eda_core": Запрос за меню
"eats-restaurant-menu" -> "eats-rest-menu-storage": Запрос за меню
"eats-restaurant-menu" <- "eda_core": Меню с дин категориями
"eats-restaurant-menu" <- "eats-rest-menu-storage": Меню без дин категорий
"eats-restaurant-menu" -> "eats-restaurant-menu": Добавление дин категорий на основе eda_core
"api-proxy" <- "eats-restaurant-menu": Отдача меню на фронт

@enduml
-->
