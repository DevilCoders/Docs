# Инстанс
Базовым компонентом платформы faas является http-сервис, написанный на Python3.
Он позволяет поднимать сразу несколько калькуляторов пользователей, каждый на своем эндпоинте.

Код инстанса располагается в [Аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/billing/hot/faas/)

## Сборка и запуск
Для того чтобы инстанс мог использовать пользовательские функции, необходимо, чтобы они и их зависимости попали
в сборку.
Общий принцип работы инстанса состоит в том, что мы можем прошить бинарь инстанса, получаемый с помощью *ya.make*, зависимостями пользовательских функций, а потом импортировать их [стандартными средствами питона](https://docs.python.org/3/library/importlib.html).

Другими словами мы можем "подложить" в бинарь самого инстанса зависимости нужной функции.

Для реализации этого используются [флаги линковки](https://wiki.yandex-team.ru/yatool/make/#zadanieflagov). С их помощью мы указываем пути до **PEERDIR** произвольных функций из [Аркадии](https://wiki.yandex-team.ru/devtools/commandsandvars/).

Сами функции-калькуляторы указываются в переменной окружения **FUNCTION**.

После запуска сервера, каждый калькулятор доступен в своем эндпоинте: `http://host/call/<name>/json`

Этот эндпоинт принимает **POST** запрос со следующей структурой
```json
{
    "event": {},
    "references": {}
}
```



### Сигнатура калькулятора
Идеологически, бизнес-логика должна описываться как чистые функции - событие на вход, транзакции на выход,
внутри калькулятора - только описание трансформации, никаких походов во внешние сервисы в калькуляторе не осуществляется.
Все данные для работы калькулятора подготавливает Процессор в соответствии с манифестом.


#### Для корректной работы калькулятора он должен соответствовать одной из следующих сигнатур

{% list tabs %}

- Функция

  {% code '/billing/hot/faas/lib/python/example/foo/foo.py' lang='py' lines='[BEGIN calculator signature]-[END calculator signature]' %}

  <small> Сигнатура калькулятора </small>

- Асинхронная функция

  {% code '/billing/hot/faas/lib/python/example/foo/foo.py' lang='py' lines='[BEGIN async calculator signature]-[END async calculator signature]' %}

  <small> Сигнатура асинхронного калькулятора </small>

- Класс с методом run

  {% code '/billing/hot/faas/lib/python/example/bar/bar.py' lang='py' lines='[BEGIN class calculator signature]-[END class calculator signature]' %}

  <small> Сигнатура калькулятора-класса </small>

- Класс с асинхронным методом run

  {% code '/billing/hot/faas/lib/python/example/bar/bar.py' lang='py' lines='[BEGIN async class calculator signature]-[END async class calculator signature]' %}

  <small> Сигнатура асинхронного калькулятора-класса </small>

{% endlist %}

В текущей версии доступны лишь калькуляторы, которые принимают и возвращают словари(данные сериализуются в JSON).

#### Формат входных и выходных данных

![alt text](../media/faas/processor_calculator.png "Взаимодействие Процессора и калькулятора")

{% list tabs %}

- Входные данные

  ```json
  {
      "event": {},
      "references": {}
  }
  ```

  В поле **event** передается само событие, которое пришло на вход в Процессор.
  В поле **references** хранятся дополнительные данные/справочники, которые были подготовлены Процессором во время подготовки события для калькулятора.

  Формат полей **event** и **references** зависят только от пользователя и настроенных им манифестов для Процессора.

- Выходные данные

  ```json
  {
      "event": {},
      "client_transactions": {}
  }
  ```

  В поле **event** передается само событие.
  В поле **client_transactions** передается массив транзакций для дальшей обработки Процессором.

  Формат полей **event** и **client_transaction** зависят только от пользователя и настроенных им манифестов для Процессора.

{% endlist %}

### Пример

{% note tip %}

В сервисе faas реализован [dummy-калькулятор](https://a.yandex-team.ru/arcadia/billing/hot/faas/lib/python/dummy), который нужен для демонстрации работы сервиса, а также для тестирования нового функционала.
Он стабилено работает и его можно использовать как для локальной сборки, так и в платформе.

{% endnote %}

1. Собираем инстанс faas
   1. Переходим в директорию [/billing/hot/faas/python](https://a.yandex-team.ru/arcadia/billing/hot/faas/python) и выполняем команду
   ```
   ➜ ya make --yt-store -D FUNCTION_PEERDIR="billing/hot/faas/lib/python/dummy"
   Ok
   ```
   С помощью флага линковки **FUNCTION_PEERDIR** указываются все зависимости функций, которые будут использоваться из данного инстанса.

   Если зависимостей несколько, то их нужно указать в одну строку через пробел
   ```
   ➜ ya make --yt-store -D FUNCTION_PEERDIR="billing/hot/faas/lib/python/dummy billing/hot/faas/lib/python/example"
   Ok
   ```
2. Указываем калькуляторы
   1. Калькуляторы описываются с помощью переменной окружения **FUNCTION**, это позволяет изменять конфигурацию инстанса
   без необходимости собирать бинарник заново. Бинарник нужно пересобирать, только если происходят изменения в коде/зависимостях.

   В переменную окружения **FUNCTION** кладется сериализованный в строку JSON массив с описанием всех калькуляторов, каждый калькулятор описывается следующей структурой
   ```json
   {
     "function": "billing.hot.faas.lib.python.dummy.dummy_calculator.dummy_calculator",
     "name": "dummy-diod",
     "settings": {
       "foo": "bar",
       "data": "dota"
     }
   }
   ```
   В поле **function** кладется путь до самой функции/класса - так как бы вы импортировали данную функцию в Python.
   В поле **name** кладется название калькулятора, это название будет использовано в эндпоинте, которому он будет соответствовать.
   В поле **settings** кладутся произвольные настройки, которые будут доступны внутри калькулятора.

   ```
   ➜ export FUNCTION='[{"function": "billing.hot.faas.lib.python.dummy.dummy_calculator.dummy_calculator", "name": "dummy-diod", "settings": {"second_setting": 43, "first_setting": "example"}}]'
   ```

   {% note warning %}

   В переменную нужно класть __сериализованную строку__, т.е. JSON нужно обернуть в кавычки

   {% endnote %}

3. Запускаем бинарный файл
   1. Бинарный файл находится в поддиректории /bin
      ```
      ➜ python ./bin/faas runserver
      ======== Running on http://127.0.0.1:8080 ========
      (Press CTRL+C to quit)
      ```
   2. Проверяем работу сервера
      ```
      ➜ curl localhost:8080/ping
      pong
      ```
   3. Отправляем запрос в калькулятор
      ```
      ➜ curl --request POST \
        --url http://localhost:8080/call/dummy-diod/json \
        --header 'Content-Type: application/json' \
        --data '{
           "event": {
             "amount": 123.4,
             "client_id": 1,
             "contract_id": 121,
             "product": "B.U. Alexandrov",
             "external_id": "122142.13422431",
             "timestamp": 1637924277
           },
           "references": {
             "contract": {
               "client_id": 1,
               "contract_id": 121
             }
           }
        }'
      {"status":"success","data":{...},"code": 200}
      ```


{% note info %}

В корневой директории (/billing/hot/faas/python) находится Makefile с подготовленными командами,
которыми можно выполнить шаги 1 и 3 с помощью шорткатов:
```
➜ make build-dummy && make runserver
```
Настраивать переменную окружения **FUNCTION** придется самостоятельно :D

{% endnote %}

## Окружение

Faas предоставляет рабочее окружение для калькуляторов.

### Context

Для работы с окружением используется объект **context**. Он хранит в себе логгер, а также настройки, которые были переданы в переменной окружения **FUNCTION**.

{% code '/billing/hot/faas/lib/python/example/foo/foo.py' lang='py' lines='[BEGIN context]-[END context]' %}

<small> Пример использования контекста </small>

### Пробрасывание ошибок

Если во время работы произойдет исключение, то оно будет отловлено инстансом и будет возвращен 500 код ответа с сообщением из исключения.

Для контролируемых исключений необходимо использовать исключение **CoreFailError**.
Данное исключение позволяет переопределить код возврата и сообщение.

```python
from billing.hot.faas.python.faas.core.exceptions import CoreFailError

def calculator(request: dict, context: Any) -> dict:
    raise CoreFailError(code=400, message="send 400 to everyone")

```
<small> Пример использования контролируемого исключения </small>


## Отладочные флаги бинарного файла

- **list**
  Выводит все импортированные калькуляторы или выводит ошибку, если калькулятор не может быть импортирован.
  - Пример
    ```
    ➜ ./bin/faas list
      dummy-diod — billing.hot.faas.lib.python.dummy.dummy_calculator.dummy_calculator
    ```
- **check**
  Проверяет, все ли калькуляторы импортируются без ошибок.
  - Пример
    ```
    ➜ python ./bin/faas check
      OK.
    ```

