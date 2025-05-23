## Сервис конфигов брокера

Хотим выселить брокерные конфиги из schema-registry чтобы разделить тестинг и прод, и вообще отвязаться от схемы.

Брокерные конфиги буду по-прежнему хранится в арккадии, но в отдельном проекте с отдельным ci.
Это значит что при обновлении/создании брокерного конфига нельзя будет ссылаться на изменения схемы из этого же pr-а.

Получается что в самом злом случае, при создании нового сервиса с новым сообщением, отправляемым в брокер, придётся сделать 3 пр-а:
* добавить сервис в карту сервисов или kafka топик или ch-кластер с правами
* добавить новое прото-сообщение в схему
* дождавшись обновления схемы, добавить брокерный конфиг
* собрать сервис

А, например, при добавлении поля, которое нужно отправлять в брокер, придётся сделать 2 пр-а, с обновлением схемы и обновлением брокер-конфига (конкретно этот случай можно упростить, расширив настройки указания полей для ch, например указывать только поля, которые отправлять не надо).

Зато мы отвязаны от кода схема-реджистри, и в будущем можем, например, использовать схемы из других источников.

### Редактирование конфигов
Храним в yaml-е, аналогично карте сервисов, в [такой](https://a.yandex-team.ru/review/2731014/files/1) структуре.
Имя стрима совпадает с путём, отдельно тестинг и прод, без общего куска (по крайней мере пока), так нагляднее.
Добавилось поле с fqdn сообщения и таймстамп.
Переименовывание конфига запрещается, поскольку требует от нас ручных действий (перенести данные в ыте), тут ничего не поменялось, проблема ха рамками этой задачи

### Валидация и публикация
Заводим новый сервис broker-conf, с grpc api и ручкой validate:
```
validate(changedConfs: List[BrokerConfig])
```

пр-триггер отправляет в broker-conf запрос на валидацию изменённых конфигов, конфиги проверяются на последней версии схемы (тут возможна гонка, когда свежезамёрженное обновление схемы ещё не докатилось до sraas, те запрос не идемпонетный, можно передавать номер версии из arc-а, но тогда пользователю придётся rebase-иться, лучше просто ретраить(?))

проверки те же, что и в анубисе, добавляется проверка на совпадение имени и пути (имя тут получается излишним, но оно удобно для поиска по аркадии)
появляется возможность писать одно и то же сообщение в разные стримы, для этого придётся передавать в каждом сообщении имя поставки
для однозначных поставок имя не нужно (по-крайней мере для обратной совместимости при миграции)

конфиги публикуются в broker-conf через релиз (гарантирует порядок)
```
publish(allConfs: List[BrokerConfig])
```
внутри broker-conf использует s3 для хранения конфигов

### Тестинг и прод

валидация тестового конфига проходит на тестовом инстансе broker-conf, а продового на продовом.
это позволяет расширять схему конфига в тестинге и менять правила валидации вначале в тестинге, потом в проде

публикация аналогично, и в тестинг и в прод, разными релизами, неработающий тестинг не блокирует обновление конфига в проде

### Использование
брокер-контроллер ходит в broker-conf за обновлениями(test -> test, prod -> prod), с номером последней известной версией, если ничего не поменялось, можно не отвечать конфигами

### Миграция
скриптецом, делаем анонс, применяем скрипт, добавляем в этот же пр дроп брокерных аннотаций, после этого выкатываем анубис, не проверяющий брокер
