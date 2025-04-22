## Order Feedback Loader

Скрипт для выгрузки, загрузки и удаления вопросов к заказу и правил задавания этих вопросов из csv

### Использование

```shell script
./feedback.py --help

# or

python3 ./feedback.py --help
```

- Куда
  - `--export` - загрузит обновления в бекенд из файла
  - `--import` - выгрузит текущее состояние из бекенда в файл
- Что
  - `--question` - грузить вопросы
  - `--rule` - грузить правила к вопросам
  - `--scenario` - грузить правила к сценариям
- Окружение
  - `--testing` - в тестинг
  - `--production` - в прод

### Формат csv

Импорт из бекенда сам создаст нужный формат csv. 
В полученной таблице первой колонкой, будет колонка `operation`. 
Колонка будет пустая.

Для загрузки в бекенд в колонку `operation` надо поместить команду `CREATE`, `DELETE` или `EDIT`. 
- `CREATE` - создать новый объект вопроса или правила в базе. 
   Поля `id`, `question.title` будут проигнорированы.
- `DELETE` - удалить объект из базы. Поле `id` обязательно.
- `EDIT` - отредактировать объект в базе. Поле `id` обязательно. `question.title` будет проигнорировано

#### Enum-ы

Для правил используются следующие перечисления:

- [PaymentMethod](https://wiki.yandex-team.ru/market/marketplace/dev/checkouter/api/entities-auto/paymentmethod)
- [PaymentType](https://wiki.yandex-team.ru/market/marketplace/dev/checkouter/api/entities-auto/paymenttype)
- [DeliveryType](https://wiki.yandex-team.ru/market/marketplace/dev/checkouter/api/entities-auto/deliverytype)

Внутри CSV можно использовать, как числовое представление (`-1`, `0`, `1`), 
так и текстовое (`UNKNOWN`, `DELIVERY`, `PICKUP`)

#### Пример

rules.csv
```csv
operation;id;question.id;question.title;showGrade;deliveryType;paymentType;paymentMethod
CREATE;2;3;Курьер был УДАЛЕН ВЫСТРЕЛОМ МИСТИЧЕСКОЙ ЛАЗЕРНОЙ ПУШКИ;4;DELIVERY;UNKNOWN;UNKNOWN
;2;3;Курьер был вежлив;4;DELIVERY;UNKNOWN;UNKNOWN
DELETE;3;127;Товар повреждён;1;UNKNOWN;UNKNOWN;UNKNOWN
```

questions.csv
```csv
operation;id;title
CREATE;1;Курьер приехал точно в срок
DELETE;2;Заказ подняли на этаж
;3;Курьер был вежлив
```

scenario.csv
```csv
CREATE;11;660;3;SORRY_REFUND;127;Товар повреждён
DELETE;12;560;3;SORRY_SUPPORT;128;Привезли не то или не все товары
EDIT;13;300;4;THANK_YOU;;
```

### echo.py

Простенький эхо-сервер, который поднимается на 8080 порте по умолчанию. 
Нужен для отладки запросов в бекенд из `feedback.py`.
