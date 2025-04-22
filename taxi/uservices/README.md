# μservices
Репозиторий с микросервисами, использующимим [μserver](https://github.yandex-team.ru/taxi/userver).

[Документация](https://wiki.yandex-team.ru/taxi/backend/userver/)

[FAQ & Quick Start](https://wiki.yandex-team.ru/taxi/backend/userver/FAQ-Quick-Start/)

Все сервисы должны располагаться в директории _./services_

Сервис-пример [./services/userver-sample](https://github.yandex-team.ru/taxi/uservices/tree/develop/services/userver-sample)

[Подробное описание создания новых сервисов](https://wiki.yandex-team.ru/taxi/backend/userver/new-service/) и скрипт их создания [./scripts/create-new-service.sh](https://github.yandex-team.ru/taxi/uservices/blob/develop/scripts/create-new-service.sh),


## Разработка
Код должен соответствовать [Google C++ Style Guide](https://h.yandex-team.ru/?https%3A//google.github.io/styleguide/cppguide) с [изменениями](https://wiki.yandex-team.ru/users/sermp/backend-cpp-codestyle/).
Код на Python должен соответствовать [Taxi Python Codestyle](https://wiki.yandex-team.ru/taxi/backend/codestyle/).
В начале работы с uservices стоит выполнить `make setup-git-hooks`

### Сборка и тестирование
Гарантируется, что сборка работает для:

  * Ubuntu Xenial c подключенным репозиторием xenial-updates/universe
  * Ubuntu Bionic c подключенным репозиторием bionic-updates/universe
  * MacOS 10.15 с установленными [Xcode](https://h.yandex-team.ru/?https%3A//apps.apple.com/us/app/xcode/id497799835) и [Homebrew](https://h.yandex-team.ru/?https%3A//brew.sh)

Гарантируется, что testsuite тесты отрабатывают без ошибок для Ubuntu Xenial.

Минимальный набор зависимостей можно установить запуском скрипта `userver/scripts/ubuntu-install-prerequisites.sh` для Ubuntu и `userver/scripts/mac-os-install-prerequisites.sh` для MacOS.

В `Makefile` для каждого сервиса автоматически определяются цели для сборки и тестирования, описанные в [документации](https://wiki.yandex-team.ru/taxi/backend/userver/makefile/).

Некоторые из целей:

  * `help` -- покажет справку по Makefile
  * `testsuite-autoenv-<service-name>` -- настраивает testsuite и запускает его, при необходимости конфигурирует и собирает сам сервис
  * `build-<service-name>` -- выполняет сборку сервиса в Debug режиме
  * `utest-<service-name>` -- собирает и запускает юнит тесты сервиса. Для вывода логов отладки нужно выставить переменную make `UNITTEST_ARGS='-l debug'`
  * `start-<service-name>` -- настраивает окружение и запускает сервис (работает только для сервисов, которые не обращаются к другим сервисам).
  * `setup-git-hooks` -- выставляет прекомитные хуки, которые автоматически форматируют код
  * `format-<service-name> check-pep8-<service-name>` -- запускает форматтер/линтер такси
  * `clean` -- удаляет результаты сборки
