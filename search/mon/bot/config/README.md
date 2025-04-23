# Configuration

Функционал бота разделен на модули. Каждый новый модуль должен быть унаследован от `BaseModule`. Конфиг модуля позволяет переопределить периодичность запуска корутин.

```yaml
# Module configuration file.

coroutines:
  <coroutine_name>:
    delay: <in_seconds>

```

## Базовая конфигурация

### development

```yaml
development: True|False # False by default
```

### security

```yaml
security:
  ca_certificate: ./config/allCAs.pem
```

### database

```yaml
max_connections: <int>  # ограничение одновременных соединений на инстанс
hosts:
  - <host>
  - <host>
port: <int> # postgres port, 5432 by default
dbname: <str> # название базы
user: <str> # пользователь, под которым нужно подключиться к базе
```

### telegram

```yaml
token: <str>  # токен, полученный от BotFather
name: <str>  # username бота
api:
  host: # host сервера MTProto
  port: # 443 по дефолту
  dc_id: # не обязательный индекс dc
  users:
    phone: # номер телефона, на который зарегистрирован аккаунт
    username: # telegram логин
    password: # если используете 2-х факт. аутентификацию

```

### web

```yaml
# параметры веб сервера
port: <int>
site: http[s]://<host>:<port>
```

## Конфигурация модулей

### bot.modules.Chart

```yaml
services_map:
  <product_name>:
    <service_name>:
      charts:
        <chart_name>: <chart_url>
```

### bot.modules.Startrek

```yaml
subscriptions:
- chats: [<chat_id>]
  queue: <name>
- chats:
  - <chat_id>
  - <chat_id>
  queue:
    name: <name>
    issues:
    - product: <product>
      service: <service>
```

### bot.modules.Global

```yaml
cast:
  disable: False|True  # вкл/выкл мартикасты
  actions_timeout: <int> # время на выполнение следующей операции
yellow:
  disable_onduty: False|True # вкл/выкл призыв дежурных во время протокола
```

### bot.modules.Support

```yaml
queues:
- <queue>  # включение очередей для создание тикетов
```

```yaml
# Кнопки сгруппированы в ряды, как того требует Telegram API.
# `delta` - объект аргументов для `datetime.timedelta`.

time_buttons:
- - name: первая кнопка 1го ряда
    delta: {minutes: m, hours: h, days: d, weeks: w}
  - name: вторая кнопка первого ряда
    delta: {...}
- - name: первая кнопка 2го ряда
    delta: {...}

services_map:
  имя_продукта_1:
    имя_сервиса_1:
      chat: id_чата
      charts:
        имя_графика_1: url_графика_1
        имя_графика_2: url_графика_2
    имя_сервиса_2:
    ...
  имя_продукта_2:
  ...
```

### Startrek

Startrek модуль не поддерживает пока никаких команд, но запускает периодическую
задачу по проверке новых задач в [Startrek](https://st.yandex-team.ru) и
оповещении заинтересованных людей или групповых чатов.

### Конфигурирование

```yaml
subscriptions:
- chats: [id_чата_1, id_чата_2]
  queues:
  - имя_очереди_1
  - name: имя_очереди_2
    issues:
      product: имя_продукта
      service: имя_сервиса
  - name: имя_очереди_3
    issues:
    - product: имя_продукта_1
      serivce: имя_продукта_1
    - product: имя_продукта_2
      serivce: имя_продукта_2
    - product: имя_продукта_3
    - service: имя_сервиса_4
```
