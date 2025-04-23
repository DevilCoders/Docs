Changelog
=========

5.1.x
-----
  * Поддержка ES6 module в `set-routes`

5.0.x
-----
  * TypeScript
  * `cookie-parser`
  * Убрана функция `requireList`
  * Класс `Model` и декораторы для документирования моделей

4.1.x
-----
  * Добавил логирование `level` в `abstract-logger`.
  * Изменение полей логирования в `duffman-http-log`:
    * `curlify` → `url`, `method`, `headers`;
    * `got` → `received`;
    * `livetime` → `request_time`;
    * Поменял обфускацию кук на `***` вместо `X` × длину строки.
  * Добавил логирование `x_request_id` в `duffman-http-log` и `duffman-access-log`.
  * Изменение полей логирования моделей в `duffman-access-log`:
    * `livetime` (`'1.234ms'`) → `time` (`'1.234'`);
    * дополнительные данные с помощью методов `core`: `logModelResolved`/`logModelRejected`.
  * `core.getServiceOptions` принимает только один аргумент и возвращает функцию.
  * В конструктор `core` можно передавать базовый класс с опциями. (Раньше обязательно надо было наследовать).

4.0.x
-----
  * Поддерживает nodejs >= 8.12
  * Удалён `ModelRequest._proxy`
  * Удалён хардкод моделей в пользу флагов `NO_AUTH`, `NO_CKEY`
  * Удалён `connection_id` из параметров моделей в `ModelRequest`
  * Убран избыточный `try`/`catch` и исправлена отправка сигнала ошибки в экспериментах
  * Удалены ошибки, не используемые напрямую Duffman'ом:
    - `RPOP_EXTERNAL_ERROR`
    - `WMI_EXTERNAL_ERROR`
    - `CALENDAR_EXTERNAL_ERROR`
    - `NO_SUCH_MESSAGE`
    - `NO_IDS`
  * Удалён `Time`
  * Обновлён `got` до версии 9.6.0
  * Изменён игнор и обработка HTTP-ошибок `core.got`
  * В `HTTP_ERROR` добавлен `response.body`
  * Обновлена имплементация `CKey`
  * `yasm` переехал в экспортируемые хэлперы
  * Обновлён `luster`
  * Добавлена ручка рестарта и настройки порта для `/ping`
  * Добавлено логирование необработанных запросов при смерти воркера
  * Опция `-c/--config` переименована в `--routes`. Добавлен дефолт `/etc/duffman/init.d`
  * Case-sensitive роутер

2.5.x
-----
  * Опция `getRaw` у `core.got`
  * Скрытие параметров в логах и `curl`
  * Подготовка к выпиливанию костылей для несуществующих моделей
    * Флаги моделей
    * Перенос костыля в отдельный метод

2.0.5
-----
  * Проверка правильных полей в retry-on-unavailable

2.0.1
-----
  * Глобальный keepAlive.

2.0.0
-----
  * `got` версии 6.7.1;
  * убрано вычисление `yaBar` из `BrowserInfo`.
