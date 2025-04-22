## Назначение
Скрипт для заказа в оркестраторе.
Работает через http API.

## Использование

### Необхоимые условия
Должены быть запущены Оркестратор и API.

### Запуск
Пример для локального запуска:
`./generic_client --skip-authentication`

Если что-то не работает, то нужно добавить ключ `-v`:
`./generic_client --skip-authentication -v`

Получение справки по параметрам:
`./generic_client --help`


Пример для тестинга
```
service_ticket=$(ya tool tvmknife get_service_ticket sshkey -s 2002740 -d 2002548)
./generic_client  --mock-payment --suburban --host=api.travel-balancer-test.yandex.net --port=80 --service-ticket=$service_ticket
```

Пример для тестинга - покупка электричек через suburban selling с тестовым контекстом
```
./generic_client --suburban --host=api.travel-balancer-test.yandex.net --port=80 --service-ticket=$(ya tool tvmknife get_service_ticket sshkey -s 2002740 -d 2002548) --suburban-selling-host="https://testing.suburban-selling.rasp.yandex.net" --mock-payment --mock-suburban
```



Локальная проверка takeout
```
./generic_client --skip-authentication --suburban --mock-payment --passport-id=424243

./generic_client --skip-authentication --suburban --mock-payment --passport-id=424243 --takeout
```
