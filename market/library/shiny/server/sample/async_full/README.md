# Сравнение производительности http-серверов

См в [./test.sh](./test.sh) если интересны детали


## Описание

- `echo_server` - Сервер задача которого просто заснуть во время обработки запроса
- `default_server` - Обычный сервер Shiny
- `async_server` - Shiny, но в качестве ядра - YT-сервер
- `raw_yt_server` - Чистый YT-сервер, без вмешательств с нашей стороны
- `userver` - uServer собственной персоной. Без каких-либо вмешательств



## Нагибатор хоста

см [IHostNagibator](./util/helpers.h) за деталями

По факту, задача: максимально "нагнуть" хостовую систему и запарарллелится насколько это возможно

Выдержка из кода: 

```     
        // CPU Intensive
        auto payload = hostNagibator.GeneratePayload(size);
        // IO + FileSystem
        hostNagibator.SavePayloadToFile(payload);
        // IO + Networking
        auto future = hostNagibator.SendPayloadToEchoServer(payload);
        // IO + FileSystem
        hostNagibator.SavePayloadToFile(payload);
        // CPU Intensive
        payload = hostNagibator.GeneratePayload(size);
        // IO + FileSystem
        hostNagibator.SavePayloadToFile(payload);
        // Await for response from echo-server 
        return future->Await();
```

Я тут пытался имитировать какую-то IO-bound работу, как это делает большинство современных web-серверов:
- В 1 запросе делаем 2 раза:
  - Что-то посчитать небольшое на CPU
  - Отправить результат в сеть асинхронно
  - Записать результат на файловую систему (асинхронно, если возможно)

#### Настройки каждого сервера:
- Потоки на прослушивание входящих соединений (для любого сервера): 4
- Потоки клиента, который стучит в echo_server: 4
- Потоки экзекутора для IO: 4 (применимо ко всем, кроме default_server)
- Очередь на обработку запросов: 5000
- логи входящих запросов включены
  - raw-yt-server почему-то не писал логов вообще

## Описание типов нагрузки и тестового стенда
Результаты лежат в папке [./images](./images)

- Вся нагрузка подавалась с помощью shiny-tank. Считаю это достаточным, т.к. Маркетный Репорт тестируется/прогревается им.
- Было два вида нагрузки, rps-base и clients-based
- Тестовый стенд: 
  - Виртуалка в QYP
  - 26 CPU
  - 64GB RAM (по факту 61.8GB)
  - 60MB/s SSD

#### rps-based нагрузка

паттерн файлов: `images/rps-<rps-count>-<server-type>`
- `<rps-count>` - кол-во rps выдаваемых одним клиентом. 1 в 1 матчится на параметр --rps в shiny_tank 
- `<server-type>` - тип сервера, см выше

| RPS  | uServer | Shiny |
| :-: | :-: | :-: |
| 50 | ![drawing](images/rps-50-userver.png) | ![drawing](images/rps-50-default-server.png) |
| 100 | ![drawing](images/rps-100-userver.png) | ![drawing](images/rps-100-default-server.png) |
| 150 | ![drawing](images/rps-150-userver.png) | ![drawing](images/rps-150-default-server.png) |

#### clients-based нагрузка

паттерн файлов: `images/clients-<clients-count>-<server-type>`
- `<clients-count>` - кол-во разных http-clients в разных потоках одновременно стреляющих в цель. 1 в 1 матчится на параметр --stream-count в shiny_tank 
- `<server-type>` - тип сервера, см выше

| Threads | uServer | Shiny |
| :-: | :-: | :-: |
| 8 | ![drawing](images/clients-8-userver.png) | ![drawing](images/clients-8-default-server.png) |
| 16 | ![drawing](images/clients-16-userver.png) | ![drawing](images/clients-16-default-server.png) |
| 32 | ![drawing](images/clients-32-userver.png) | ![drawing](images/clients-32-default-server.png) |


