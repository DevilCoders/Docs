# Фронтенд сервиса Яндекс.Помощь

Лендинг с возможностью доната. [Фигма](https://www.figma.com/file/z0ZbbNFpVg8oKlIf2tyWqP/Яндекс.Помощь?node-id=0%3A1)

## Хосты

[Сервис в Tariff Editor](https://tariff-editor.taxi.yandex-team.ru/services/2/edit/354573/deployments)

* unstable - [helpnearby.taxi.dev.yandex.ru](https://helpnearby.taxi.dev.yandex.ru/)
* unstable-01 - [helpnearby-unstable-01.taxi.dev.yandex.ru](https://helpnearby-unstable-01.taxi.dev.yandex.ru)
* testing - [helpnearby.taxi.tst.yandex.ru](https://helpnearby.taxi.tst.yandex.ru/)
* stable - [help.yandex.ru](https://help.yandex.ru/)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing.

- [Фронтенд сервиса Яндекс.Помощь](#фронтенд-сервиса-яндекспомощь)
  - [Хосты](#хосты)
  - [Подготовка](#подготовка)
  - [Установка и запуск](#установка-и-запуск)
  - [Вопросы безопасности](#вопросы-безопасности)
    - [Закрываем хэлсчеки от внешних пользователей](#закрываем-хэлсчеки-от-внешних-пользователей)
    - [Делимся секретами для локальной разработки с командой](#делимся-секретами-для-локальной-разработки-с-командой)
  - [Доступные команды](#доступные-команды)
  - [Документация](#документация)
  - [Релиз](#релиз)
  - [Полезные ссылки](#полезные-ссылки)
  - [Логи](#логи)

## Подготовка

Для работы потребуется Node.js 10.

Для начала [устанавливаем Brew](https://wiki.yandex-team.ru/spec/devops/kakustanovitbrew/). Затем:

```bash
# Устанавливаем NVM (не забываем выполнить инструкции от Brew в секции Caveats)
brew install nvm

# Устанавливаем Node.js 10 версии
nvm install 10
```

## Установка и запуск

```bash
# Устанавливаем зависимости
npm run deps
```

Скачайте `.tvm.json` из [yav](https://yav.yandex-team.ru/secret/sec-01ej3d0zvsg9x7vjnpzdhvjs90) и положите в корень сервиса.

```bash
# Запускаем приложение (magicdev запросит ваш пароль, чтобы запустить его на 443 порту).
# По необходимости, вы можете задать другой порт, не требующий sudo, в файле .magicdev.json.
npm run dev
```

Проект становится доступен по адресу:
https://localhost.msup.yandex.ru:8081/

## Вопросы безопасности

### Закрываем хэлсчеки от внешних пользователей

Из коробки стаб предлагает хелсчеки для отслеживания состояния необходимых смежных сервисов (например, доступность чёрного ящика, геобазы и базы данных). Пути, за которыми они скрыты, могут быть использованы для создания HTTP juggler-проверок в Qloud.

> :warning: Для того, чтобы эти пути не стали доступны внешним пользователям на публичном домене, необходимо в Qloud создать путь `/healthchecks/` и направить его в компоненту типа _http-balancer_, в параметре _Servers_ указав `http://any.yandex.ru/`.

### Делимся секретами для локальной разработки с командой

В результате генерации создан не публичный файл _.tvm.json_, который хранит настройки утилиты для раздачи TVM тикетов.

> :warning: Ни в коем случае не публикуйте этот файл в репозиторий! Для того, чтобы поделиться им с командой [заведите хранилище](https://wiki.yandex-team.ru/security/secdist/#formanazavedeniezajavki) в Secdist и [разместите его](https://wiki.yandex-team.ru/security/secdist/#rabotasobychnymifajjlamiproektnajapapka) в нём.

## Доступные команды

Команда | Действие
------------ | -------------
deps | Установка зависимостей
dev | Запуск tvmtool и приложения для локальной разработки
build | Запуск production сборки скриптов и стилей
lint | Проверка TypeScript и CSS кода на codestyle
test | Запуск тестов
jest | Запуск unit-тестов вручную (todo [полноценная интеграция в ci/cd](https://st.yandex-team.ru/POMOSHDEV-743))

## Документация

* [Гайды по использованию проектов на основе Project Stub](https://wiki.yandex-team.ru/toolbox/project-stub/)

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)

## Полезные ссылки

[Эксперимент с блоками](https://tariff-editor.taxi.tst.yandex-team.ru/experiments3/experiments/show/helpnearby_mobile_constructor2/current?consumer=helpnearby_client&enabled=all&active=all&order=created_desc&is_technical=all&removed=without_removed&name=help)
[Бункер](https://bunker.yandex-team.ru/health-helpnearby/pages)


## Логи
[Тестинг](https://kibana.taxi.tst.yandex-team.ru/goto/d5841104eb1baf8f14fe098bb5373673)
[Прод](https://kibana.taxi.yandex-team.ru/goto/c1c32ec50670850102bf0396fe82f507)
