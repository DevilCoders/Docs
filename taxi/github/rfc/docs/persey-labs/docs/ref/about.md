# Сводка операций API

Хост для всех запросов к API — `labs-api.yandex.ru`. 

{% note warning "Внимание!" %}
API поддерживает работу только по протоколу HTTPS.
{% endnote %}

Ниже приведена таблица операций, которые доступны в API.

| Операция |  Описание      |
| ------------- |--------------|
|  [GET /lab/v1/buckets](get-buckets.md)   |  Получить список заявок на определенный день. |
|  [GET /lab/v1/labs](get-labs-list.md)   |  Получить список отделений. |
|  [PUT /lab/v1/orders/barcode](put-barcode.md)  | Сохранить штрихкод заявки. |
|  [PUT /lab/v1/status](set-lab-status.md)  | Обновить статус заявки. |