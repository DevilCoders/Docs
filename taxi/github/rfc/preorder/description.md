#Описание работы предзаказа

## preorder_availability - новая ручка
  - новая ручка в протоколе (py3) для возвращения данных для барабана с датой и временем
  - идет в ручку ML за интервалами и возвращает их клиенту с таймзоной
  - клиент сам разбирается, в какой таймзоне отображать интервалы
  
## routestats
  - принимать новое требование (отложенный заказ)
  - не учитывать сурж
  - проверять что в поле due валидное время (ходить в ручку preorder_availible), на которое можно сделать заказ, если на данное время нельзя заказать - не отдавать цену на данный тариф 3d
  - получить маршрут без пробок, считать цену по нему.
  - вернуть цену в формате От {calculated_price}
  TAXIBACKEND-21850 3d
## orderdraft/ordercommit
  - проверять новое требование и due 1d
## launch
  - искать не только текущие заказы, но и будущие заказы
  - нужно научиться не раскрывать некоторые заказы (которые на будущее) в карточку заказа по флагу 1d
## orderhistory
  - получать список будущих заказов 1d
## requestconfirm?
- нужно уметь отменять заказ и нужно проверить что ручки change* работают корректно 2d

# API ручек ML и py3 protocol
  - ML: <https://github.yandex-team.ru/explorer/backend-cpp/blob/develop/ml/docs/yaml/preorder_available.yaml>
  - taxi-protocol: <https://github.yandex-team.ru/ekatsevman/backend-py3/blob/feature/21851-preorder-handle-simple/taxi-protocol/taxi_protocol/docs/api/preorder_availability.yaml>