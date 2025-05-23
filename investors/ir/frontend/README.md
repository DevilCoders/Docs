# ir-www

- [Подготовка](#Подготовка)
- [Установка и запуск](#Установка-и-запуск)
- [Вопросы безопасности](#Вопросы-безопасности)
    - [Закрываем хэлсчеки от внешних пользователей](#Закрываем-хэлсчеки-от-внешних-пользователей)
    - [Делимся секретами для локальной разработки с командой](#Делимся-секретами-для-локальной-разработки-с-командой)
- [Мониторинги](#Мониторинги)
- [Доступные команды](#Доступные-команды)
- [Документация](#Документация)

## Подготовка

Для работы потребуется Node.js 12.

Для начала [устанавливаем Brew](https://wiki.yandex-team.ru/spec/devops/kakustanovitbrew/). Затем:

```bash
# Устанавливаем NVM (не забываем выполнить инструкции от Brew в секции Caveats)
brew install nvm

# Устанавливаем Node.js 12 версии
nvm install 12
```

## Установка и запуск

В корне проекта создать файл `.tvm.json` с содержимым из [секрета](https://yav.yandex-team.ru/secret/sec-01fs70p4n6excpcgfnt27r043r).

```bash
# Устанавливаем зависимости
npm run deps

# Запускаем приложение (magicdev запросит ваш пароль, чтобы запустить его на 443 порту).
# По необходимости, вы может задать другой порт, не требующий sudo, в файле .magicdev.json.
npm run dev
```

Проект становится доступен по адресу:
https://localhost.msup.yandex.ru/

## Вопросы безопасности

### Закрываем хэлсчеки от внешних пользователей

Из коробки стаб предлагает хелсчеки для отслеживания состояния необходимых смежных сервисов (например, доступность чёрного ящика, геобазы и базы данных). Пути, за которыми они скрыты, могут быть использованы для создания HTTP juggler-проверок в Qloud.

> :warning: Для того, чтобы эти пути не стали доступны внешним пользователям на публичном домене, необходимо в Qloud создать путь `/healthchecks/` и направить его в компоненту типа _http-balancer_, в параметре _Servers_ указав `http://any.yandex.ru/`.

### Делимся секретами для локальной разработки с командой

В результате генерации создан не публичный файл _.tvm.json_, который хранит настройки утилиты для раздачи TVM тикетов. Содержимое `.tvm.json` хранится [тут](https://yav.yandex-team.ru/secret/sec-01fs70p4n6excpcgfnt27r043r).

> :warning: Ни в коем случае не публикуйте этот файл в репозиторий!



# Мониторинги

В файле [.monitorado.yml](./.monitorado.yml) находится конфиг с настройками для мониторингов.
Про формат конфига и утилиту Monitorado можно почитать в [документации](https://github.yandex-team.ru/toolbox/monitorado).

> :bulb: Если мониторинги срабатывают слишком часто, просто поменяйте граничные значения в конфиге и заново запустите настройку.

Команды для управления мониторингами перечислены ниже.

> :warning: Не забудьте получить все необходимые [токены](https://github.yandex-team.ru/toolbox/monitorado#Токены).



## Доступные команды

Команда | Действие
------------ | -------------
deps | Установка зависимостей
dev | Запуск tvmtool и приложения для локальной разработки
build | Запуск production сборки скриптов и стилей
lint | Проверка TypeScript и CSS кода на codestyle
test | Запуск тестов
monitoring:diff | Показывает, что будет сделано при настройке мониторингов
monitoring:exec | Настраивает мониторинги согласно конфигу


## Документация

* [Гайды по использованию проектов на основе Project Stub](https://wiki.yandex-team.ru/toolbox/project-stub/)
