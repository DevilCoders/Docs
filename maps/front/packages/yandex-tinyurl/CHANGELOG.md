## 3.1.0

* Add TypeScript declaration file ([#23](https://github.yandex-team.ru/maps/yandex-tinyurl/pull/23)).

## 3.0.0
* Библиотека [asker](https://github.com/nodules/asker) заменена на [request](https://github.com/request/request) ([#19](https://github.yandex-team.ru/maps/yandex-tinyurl/pull/19))
* Методы `YandexTinyurl#store` и `YandexTinyurl#retrieve` возвращают нативный `Promise` вместо `vow.Promise`.
* Минимально поддерживаемая версия `Node.js` обновлена до `0.12`.

## 2.4.0
* Добавлена опция `ipFamily` в конструктор `Tinyurl`.

## 2.3.0
* Timeout в запросах к сервису tinyurl увеличен с 500 мс до 5 с.

## 2.2.0
* Используются POST запросы к сервису tinyurl.

## 2.1.0
* Используется json формат ответа сервиса tinyurl.

## 2.0.1
* Пакет xml2json заменен на xml-parser.

## 2.0.0
* Опция host переименована в url. Требуется передавать полный URL до сервиса.

## 1.0.2
* Отключена опция `sanitize` при переводе xml в json.

## 1.0.1
* Опции конструктора стали не обязательны.
* Исправлена ошибка с учетом имени хоста, если хост передан без слеша в окончании.

## 1.0.0
* Первая версия.
