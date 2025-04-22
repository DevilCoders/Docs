# Задачи
# 1. [corp-billing] Ручки pay-order, close-order
Аналогично Еде сделать ручки 
* v1/pay-order/tanker
* v1/close-order/tanker  
https://a.yandex-team.ru/arc_vcs/taxi/uservices/services/corp-billing/docs/yaml/api/payments.yaml
# 2. [corp-billing] Обрабатывать топики Заправок в v1/billing-orders
Сделать аналогично другим сервисам  
https://a.yandex-team.ru/arc_vcs/taxi/uservices/services/corp-billing/src/views/v1/billing-orders
# 3. [corp-billing] dist lock компонента для ивентов Заправок:
billing_tanker_sync_dist_lock  
аналогично другим сервисам  
https://a.yandex-team.ru/arc_vcs/taxi/uservices/services/corp-billing/src/components
# 4. [corp-orders] Сохранять заказы в постгрес
Нужно написать  
* крон create_tanker_order
* stq corp_create_tanker_order (нужна ручка от Заправок)
* схему таблички corp_order.tanker_orders
* ручку v1/orders/tanker/find и если нужно v1/order/tanker/find
# 5. [corp-int-api] payment-methods для Заправок
Нужно
* Ручка /v1/payment-methods/tanker аналогично Еде (пока зависит от выбранного способа синхронизации сотрудников)
* Обновить лимиты: потраченное за день/месяц
* Добавить лимит на тип топлива, но сперва понять как работать с их многообразием
# 6. [taxi-corp] Заправки в ЛК
* Для раздела в Поездки и отчёты в кабинете нужна будет ручка 
1.0/client/{client_id}/tanker/orders
* 1.0/client/{client_id} в поле services в ответе учитывать сервис заправок
* GET и POST 1.0/client/{client_id}/user. 
  Подключение/отключение сервиса сотруднику.
  Сейчас в интерфейсе можно задать
только месячный лимит, но вроде бы у нас есть поддержка дневных лимитов
* 1.0/client/{client_id}/user/{user_id}/order — сейчас возвращает заказы Такси
конкретного сотрудника. Просят сделать то же самое для Заправок.
* 1.0/client/{client_id}/reports/orders/generate — скачать реестр заправок за месяц
# 7. [taxi-corp-admin] Заправки в Админке
проверить, и если нужно добавить поддержку сервиса
* v1/clients/list — поле services в ответе
* v1/contracts — поле services
* v1/services
* v1/clients/{client_id}/reports/acts/generate — добавить sheet в ДА
* v1/clients/{client_id}/reports/orders/generate — добавить поддержку tanker
* v1/users