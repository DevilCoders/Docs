# POST прокси ручка для поллинга заказов лавки и еды

задача: https://st.yandex-team.ru/TAXIBACKEND-33683

Проблема:
- Ручка полинга статуса заказа лавки ходит в кэш, при отстутсвии известных заказов в запросе, из-за этого, иногда, заказы лавки могут пропадать с главного экрана в ГО после создания.

## Решение
- Делаем POST ручку, и добавляем в запросе передаём известные заказы
- в `superapp_parameters` в корень добавляем доп параметр `tracking_method` показывающий какой метод запроса использовать для ручки трекинга: `post` - используем post ручку с body, `get` или отстуствие данного параметра - используем GET ручку без body.

[API новой ручки](orders_proxy_post.yaml)

## Бэкенд
1. Обобщить код и реализовать новую ручку с проксированием параметров + тестирование [1.5d]
