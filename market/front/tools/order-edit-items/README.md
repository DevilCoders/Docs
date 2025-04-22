# order-edit-items

Простенький скрипт для удаления товара из заказа

Для работы скрипта требуется созданный заказ, который поддерживает удаление товара.

Неплохим стартом является (был) вот этот [товар](https://desktop.bluemarket.fslb.beru.ru/product/miagkaia-igrushka-hansa-morzh-22-sm/216800597). 
Утверждается, что его лучше брать со склада `172` (выбери через кнопку дебага).
На момент написания README обязательным является наличие rearr-флага `items_removal_if_missing=1`

Больше подробностей [тут](https://wiki.yandex-team.ru/users/krauklis/Testplan-udalenija-tovarov-iz-zakaza/#kaksdelatzakazdljaproverki)
и [тут](https://wiki.yandex-team.ru/users/skutyev/Udalenie-chasti-zakaza-s-tochki-zrenija-Chekautera/#kontrakt)

## edit.py

Собственно, тула. 
- Сбегает в чекаутер за заказом, получит товары из него
- Сбегает в чекаутер за проверкой, что товары можно удалять
- Сбегает в чекаутер с попыткой удалить товары
- Сбегает в чекаутер с апрувом на удаление

Внимание: требует установки библиотеки [`requests`](https://requests.readthedocs.io/en/master/user/install/) для отправки запросов (например, через PIP или Conda)

Формат параметров ниже

**Важно**. Питонский `arg_parse` говорит, что `orderId` должен идти после `--items`. Врёт. Перед. 

```
usage: edit.py orderId [-h] [--items [ITEMS [ITEMS ...]]]

Simple tool to remove items from checkout order. This tool sends the bunch of
queries to amend order

positional arguments:
  orderId               Id of order to amend to

optional arguments:
  -h, --help            show this help message and exit
  --items [ITEMS [ITEMS ...]], -i [ITEMS [ITEMS ...]]
                        Items to amend. You can set the position of item in
                        the list. Format is: `${item_idx}:${item_remained}`.
                        `item_idx` is 0-based index of item in the order.
                        `item_remained` is count of item. Use 0 to remove
                        item, use -N to subtract count of item. Default value
                        is `0:-1`, which means take the first item and
                        substract it count by 1
```

## echo.py

Простенький эхо-сервер для отладки. Не нужен для непосредственной работы с чекаутером, не используется в работе скрипта
