# Нотификации: пора заказывать такси (MVP)

## Описание

Пользователь указывает точку А и Б, и дату и время, когда он планирует приехать в заданную точку, бек должен прислать пользователю пуш, о том, что если в течениии 5 минут пользователь не закажет такси, то может опоздать



## Как это будет работать с клиентской части

![](https://wf.yandex-team.ru/plantuml/RP71IWCn48RlynH3xheUFFKWHRnNqBjaCoc4TfEIZOAtTf7s7NoA8XONfJx3v8rCThLiYwT9_dpCV4p6TP0-F5Ppa2euZu9V-OjRtl4-DW9bZMfkj0q0YyGPPHRI1XGJJzgZTS5Cdx7M_iaetT7E0iaWIrdh4-hckWEe1EXRujbLmaSenEtaxXwBo_EBecSByd8QX01dCqJb2EEAl_c3ttdBkzXWtAIov7qAtvBj9-PZRBYDB_dAsxXEjGKg_wRqdHyC_JRj7ORv_rg7zoD1vQhA71jMqiy6TDvS1saQMBZPoVWKm5XRoZ_m0m00)


Для организации идемпотентности будет две клиетские ручки:
* /4.0/notify/draft, которая проверит входные данные и создаст в базе черновик нотификации
* /4.0/notify/commit, которая пометит черновик как закомиченным (иначе крон удалит этот черновик через некоторое время)


## /4.0/notify/draft

Данная ручка должна получать на вход следующие данные:
* User_id для возможности отправки пуша на нужный девайс
* Accept-Language - для текста сообщения в пуше
* X-Request-Application приложение необходимое для пуша
* в body:
    * массив из точек routes (как в routestats)
    * target_class - требуемый тариф
    * target_date - дата назначения


Что делает ручка:
* Идет в сервис taxi-tariffs за настройками зоны и чекает валидность тарифа
* Ходит в ручку /eta сервиса driver-eta для получения времени прибытия водителя
* Идет в граф\карты (кажется, что получить дырки до графа проще чем до карт) за времем поездки
* Суммирует все время и проверяет, что разница между запланированным временем и текущим больше чем время поездки + ожидание водителя (наверно тут еще надо прибавлять какое-нибудь время бесплатноог ожидания)
* Создает черновик в базе
* Возвращает идентификатор черновика




## /4.0/notify/commit

Принимает на вход идентификатор черновика

Что делает:
* Помечает заказ в базе как закомиченный
* Планирует stq таску order_notify на время равное запланированная дата - (2 * время поездки) (тут можно еще какие-то эвристики придумать)



## stq order_notify

* Идет в ручку GET /internal/notify за данными по нотификации
* Идет в граф за временем поездки
* Идет в ручку /eta за временем прибытия водителя
* Если до отправки остается меньше чем 5 минут (будет настраиваться в конфиге наверно), то идем в ручку /internal/notify/mark_done, чтобы отметиться что мы отправили пуш
* Идем в ручку /user/notification/push и отправляем пуш

Если до отправки остается больше, то перепланируемся через 5 минут (тут опять же есть место эвристикам)



## База

```postgresql
CREATE TABLE order_notify
(
  notify_id       TEXT        NOT NULL,
  user_id         TEXT        NOT NULL,
  application     TEXT        NOT NULL,
  accept_language TEXT        NOT NULL,
  notify_data     JSONB       NOT NULL,
  status          TEXT        NOT NULL,
  type            TEXT        NOT NULL,
  commited        BOOLEAN     NOT NULL,
  created         TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated         TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  PRIMARY KEY (notify_id)
);
```

