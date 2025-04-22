# currency-import-tool - импорт списка валют из Директа

### Описание
Валюты и всяческие константы, связанные с ними, хранятся перловом Директе.
Утилита ходит в intapi Директа, получает оттуда данные, сохраняет в Аркадию.
Генерируется интерфейс, описывающие все валютные константы, курсы и набор классов (по одному для каждой валюты), его реализующих.
Предполагается периодический запуск руками одного из разработчиков, в рамках задачи изменения информации о валютах.

Перловая часть см. Intapi::CurrenciesList и jsonrpc/CurrencyRates?method=get_YND_FIXED_rates.


### Использование
При появлении новой валюты - сначала добавить её в CurrencyCode (libs/currency)

При появлении новых констант - для неденежных констант - добавить их тип в `CurrencyImporter#getTypeByField` и `CurrencyImporter#makeClassField`

Запустить импорт: `./currency-import-tool.sh http://8998.beta1.direct.yandex.ru/CurrenciesList http://8998.beta1.direct.yandex.ru/jsonrpc/CurrencyRates?method=get_YND_FIXED_rates`

Затем вручную сделать *Optimize Imports* из IDEA
в `libs/currency/src/main/java/ru/yandex/direct/currency/currencies/*.java`
и `currency/src/main/java/ru/yandex/direct/currency/Currency.java`.
*(в будущем возможно сделаем аннотации для исключений jstyle или отключим проверку на весь модуль)*

Не забыть закоммитить новые изменения.
Если появлялись новые валюты - добавить файлы (в SVN), добавить инстанс валюты в Currencies, код валюты в DirectCurrenciesTest
