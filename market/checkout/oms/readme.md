# Этот проект - MVP сервиса управления заказом маркета.
Все, что здесь написано, не является окончательным решением или правилом.
Все пишется для примера и дальнейшего согласования.
#Правила разработки

## Типы
* Время - в коде OffsetDataTime, в базе timestamptz (пока что это не так)
* Деньги - long (пока что float в коде)
## Общие подходы
* Используем OpenAPI, JOOQ
* Один статический инстанс маппера. Если получается гиганский класс маппера то пилим его на домены
* Используем везде Сlock никаих Instant.now() в коде (пока что это не так)
* Бины не автовайрим. Все через private final и RequiredArgsConstructor
* Сдвигаем границу транзакции максимально близко к репозиторию
* Код класса помещается на один экран ноутбука

## Чтобы локально запустить
1. Получить токен https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982
2. Положить в переменную окружения mj.yav.oauth-token

## Кто хранит секреты?
Сейчас секреты получаются от лица https://staff.yandex-team.ru/zomb-emily, соответственно и токен в секретах этого лица.
Секрет с токеном https://yav.yandex-team.ru/secret/sec-01g80mdcpptn3rjdzahq0dff1s/explore/version/ver-01g80mdcq7js8p1w4bw0fghhrr

## Чтобы работать с экспериментами локально
1. Установить докер https://wiki.yandex-team.ru/zen/tech/development/docker/?from=%2Fzen%2Ftech%2Fdevichwill%2Fdocker%2F#ustanovka
2. Запустить docker-compose up -d
3. Документация по админке конфигов https://wiki.yandex-team.ru/users/barinovale/postigaem-neizvestnoe/adminkakonfigov/

## Работать с транзакциями
По классике transactionTemplate - для записи, readonlyTransactionTemplate - для чтения

## Работать с пропертями
1. Общие свойства пишутся в 00_application.properties, переопределяются в соответствующих папках в зависимости от environment
2. Если в ConfigurationProperties указано поле Object someField, в пропертях оно должно быть записано some-field

## TVM
1. Получить тикет для тестинга ya tool tvmknife get_service_ticket sshkey -s 2033857 -d 2035279
2. Заголовочный параметр X-Ya-Service-Ticket

## TODO ПЕРЕРАБОТАТЬ ЭТОТ ФАЙЛ, РАЗБИТЬ НА ПОДКАТЕГОРИИ И ТД
