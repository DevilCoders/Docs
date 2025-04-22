# Кратко про бекенд

Разработка бекенда в основном ведется на C++, поэтому в первую очередь необходимо изучить требования к оформлению C++ кода: [Arcadia C++ Style Guide](https://docs.yandex-team.ru/arcadia-cpp/cpp_style_guide). Основные выжимки:
* CamelCase
* Префикс T для имен классов, префикс I – для интерфейсов, E – для enum'ов
* Blame-driven development: много в оформлении кода выбирается таким образом, чтобы менять минимальное число строк кода при расширении функционала

## Сервисы бекенда

Сервисы бекенда разделяются на 3 основных контура:
 * testing &mdash; тестовый контур бекенда.
 * prestable &mdash; предрелизный контур бекенда. На нем обычно крутятся свежие ревизии бекенда.
 * stable &mdash; релизный контур бекенда. Это основной контур бекенда, который обслуживает всю функциональность бекенда. Он разделяется на следующие сервисы:
   - [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/drive_backend_stable/) &mdash; API для клиентского приложения.
   - [admin](https://nanny.yandex-team.ru/ui/#/services/catalog/drive_backend_admin/) &mdash; API для админки.
   - [chat](https://nanny.yandex-team.ru/ui/#/services/catalog/drive_backend_chat/) &mdash; API для чатов клиентского приложения.
   - [service_app](https://nanny.yandex-team.ru/ui/#/services/catalog/drive_backend_service_app/) &mdash; API для сервисного приложения.
   - [robot](https://nanny.yandex-team.ru/ui/#/services/catalog/rtline_drive_frontend_robot/) &mdash; сервис для фоновых процессов (роботов).

## Основные идеи

### Базовые объекты

К базовым объектам можно отнести:

* Пользовать.
* Машина.
* Заказ (текущая сессия и завершенная сессия).

### Теги

Теги &mdash; это дополнительные свойства для базовых объектов. Логично предположить что теги бывают пользовательскими (`user_tags`), для машин (`car_tags`) для сессий (`trace_tags`).