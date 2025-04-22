# API 1.0

Для вызова методов API версии 1.0 используйте хост:

```
https://business.taxi.yandex.ru/api/...
```

Ниже приведен список запросов к сервису Яндекс Такси для версии API 1.0:

Адрес запроса | Метод | Описание
----- | ----- | -----
/auth | GET | [Информация о клиенте](auth.md)
/oauth/refresh | GET | [Обновить OAuth-токен](oauth-refresh.md)
/1.0/class | GET | [Список тарифов](class-list.md)
/1.0/client/{client_id} | GET | [Детальная информация о клиенте](client-info.md)
/1.0/client/{client_id}/cost_centers | POST | [Создание кост-центров клиента](cost-center-create.md)
/1.0/client/{client_id}/cost_centers | GET | [Список настроек кост-центров](cost-center-settings-list.md)
/1.0/client/{client_id}/cost_centers | PUT | [Создание кост-центров клиента в старом формате](cost-center-create-old.md)
/1.0/estimate | POST | [Получить информацию о предстоящей поездке](route-stats.md)
/1.0/client/{client_id}/order | GET | [Список заказов](order-list.md)
/1.0/client/{client_id}/order | POST | [Создание черновика нового заказа](order-create.md)
/1.0/client/{client_id}/order/{order_id} | GET | [Детальная информация о заказе](order-info.md)
/1.0/client/{client_id}/order/{order_id}/cancel | POST | [Отменить заказ](order-cancel.md)
/1.0/client/{client_id}/order/{order_id}/progress | GET | [Отслеживание заказа](order-progress.md)
/1.0/client/{client_id}/order/{order_id}/processing | POST | [Обработка заказа](processing.md)
/1.0/client/{client_id}/order/{order_id}/change | PUT | [Изменить данные черновика заказа](order-change.md)
/1.0/client/{client_id}/role | GET | [Список ролей сотрудников](role-list.md)
/1.0/client/{client_id}/role | POST | [Создание новой роли](role-create.md)
/1.0/client/{client_id}/role/{role_id} | GET | [Детальная информация о роли](role-info.md)
/1.0/client/{client_id}/role/{role_id} | PUT | [Редактирование роли](role-edit.md)
/1.0/client/{client_id}/role/{role_id} | DELETE | [Удаление роли](role-delete.md)
/1.0/client/{client_id}/user | GET | [Список пользователей клиента](user-list.md)
/1.0/client/{client_id}/user | POST | [Создание нового пользователя](user-create.md)
/1.0/client/{client_id}/user/{user_id} | GET | [Детальная информация о пользователе](user-info.md)
/1.0/client/{client_id}/user/{user_id} | PUT | [Обновление данных пользователя](user-update.md)
/1.0/client/{client_id}/user/{user_id} | DELETE | [Удалить пользователя](user-delete.md)
/1.0/client/{client_id}/user/{user_id}/restore | PUT | [Восстановление пользователя](user-restore.md)
/1.0/client/{client_id}/geo_restrictions | GET | [Список районов](region-list.md)
/1.0/client/{client_id}/geo_restrictions | POST | [Создание нового района](region-create.md)
/1.0/client/{client_id}/geo_restrictions/{geo_id} | PUT | [Изменение района](region-edit.md)
/1.0/client/{client_id}/geo_restrictions/{geo_id} | DELETE | [Удаление района](region-delete.md)


