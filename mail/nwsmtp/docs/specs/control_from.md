Контроль From
=======

Механизм проверки заголовка From/Sender на соответствие авторизованному отправителю.

## Общий алгоритм:

1. Выбирается заголовок:
    * если есть Sender, то выбирается он
    * иначе первый From в порядке появления
2. Выбирается адрес:
    * Если не удалось найти адрес в заголовке, то проверка завершается ошибкой
3. Выполняется поиск уида в черном ящике для адреса из заголовка
4. Если пользователь в черном ящике не найден, то проверка завершается ошибкой
5. Сверяются uid авторизованного отправителя и uid адреса из заголовка
    * если совпадают, то проверка завершается успехом
    * иначе фейлом

## Алгоритм работы с белыми списками:
Если проверка завершилась фейлом или ошибкой, то для авторизованного отправителя выполняется:
1. Дла ПДД пользователя проверка на вхождение домена в белый список доменов
2. Для остальных - проверка на вхождение uid-а в список uid-ов.

Если домен или уид находятся в списке, то проверка завершается успехом.

### Как обновлять белые списки?
Они хранятся в виде ресурсов:
https://a.yandex-team.ru/arc/trunk/arcadia/mail/nwsmtp/control_from/ya.make?rev=7120793#L1
1. Нужно обновить список в ресурсе или создать новый ресурс
    * не забыть пометить ресурс как неудаляемый 
2. Заменить идентификатор ресурса в ya.make
3. Пересобрать пакет с конфигами или образ
