# IMS коннектор к StaffAPI

## Запуск
Producer
```shell
python staff_connector producer *HANDLER_NAME*
```

Consumer
```shell
python staff_connector consumer *HANDLER_NAME* [--]
```

## Handler-ы
 * **ping** - тестовые запись/чтение из очереди
 * **user** - выгрузка пользователей из Staff API
