## Структура модулей

![](modules.png)

### Web

#### Внешнее API

создание, удаление, редактирование сборщиков

локально или с проксированием на другие машины (шардирования)

проксирование в кластер внешних сборщиков

#### Внутреннее API

отдает данные из mailbox

### Sharder

список баз и пользоватей

распределение пользователей по машинам

### Auth

проверять OAuth токены

получать инфо о пользователе

редактирование email алиасов пользователя

### Streamer

загружает и выгружает сборщики в планировщик

создание, удаление, редактирование сборщиков

#### Planner

циклично и последовательно запускает абстрактные задачи

можно добавить, отменить, остановить задачу по ID

#### Operations

main op в зависимости от состояния сборщика запускает дочерние операции

инициазация

миграция (в обе стороны)

сбор почты

удаление

## Collectors db

хранение и редактирование метаданных о сборщике

## Mailbox

### xdb

чтение и запись почтовых метаданных

покладка собранных писем

### http

только чтение почтовых метаданных