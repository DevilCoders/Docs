# Общие паспортные компоненты

## Компоненты

* [commander](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/commander) - создание CLI паспортных инструментов
* [configurator](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/configurator) - чтение файлов конфигурации в приложениях
* [distprim](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/ea) - примитивы для распределенной работы
* [ea](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/ea) - обработка потоков событий с подсчетом статистик
* [errors](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/errors) - общие паспортные ошибки
* [historydbloader](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/historydbloader) - загрузчик данных в Passport HistoryDB
* [isort](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/isort) - isort, переделанный под платформонезависимую сортировку и интегрированный с commander
* [langdetect](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/langdetect) - завендореная библиотека для работы с cookiemy
* [log](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/log) - общие паспортные инструменты логирования
* [loki](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/loki) - менеджер воркеров для WSGI сервера bjoern
* [nginx_config_generator](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/nginx_config_generator) - шаблонизатор конфигов nginx
* [netree](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/netree) - дерево для хранения сетей и подсетей с проверкой вхождения заданного IP в сети и с хранением аттрибутов для подсетей
* [packaging](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/packaging) - библиотека для пакетирования паспортных проектов
* [repo](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/repo) - библиотека работы с репозиторием
* [tensornet](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/tensornet) - враппер для бинарника tensornet
* [test](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/test) - общие паспортные инструменты тестирования
* [wsgi_runner](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/wsgi_runner) - запуск WSGI приложений
* [yalearn](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library/yalearn) - структуры для обработки потока событий

## Правила разработки

* Для нового кода должно быть 100% покрытие тестами
* Пишите и поддерживайте документацию в актуальном состоянии
