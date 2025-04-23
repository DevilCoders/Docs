# Logbroker Consumer HOWTO

Для использования Logbroker Consumer в виде компонента следайте следующее:

* Запросите client-id для вашего сервиса в стартреке (пример: https://st.yandex-team.ru/DATA-931).  Учтите, что выделение айдишника может затянуться на несколько дней.

* Проверьте данные вашего топика и client-id с помощью утилиты `logbroker-perf` (`common/tools/logbroker_consumer_perf/`).  Она считывает данные из ЛБ и сохраняет их в файл.

* Добавьте поле типа `Value<config::LogbrokerConsumerComponentSettings>` в конфиг и в `backend-cpp/common/configs/declarations/`.

* Используйте класс `LogbrokerConsumerComponent` для чтения.  В конфиге fastcgi пропишите ему ident, log_type, client_id.

