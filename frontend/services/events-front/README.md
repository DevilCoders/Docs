# events-front

[![Build Status](https://drone.yandex-team.ru/api/badges/montserrat/events-front/status.svg?branch=dev)](https://drone.yandex-team.ru/montserrat/events-front) [![OKO health](https://oko.yandex-team.ru/badges/repo.svg?repoName=frontend/services/events-front&vcs=arc)](https://oko.yandex-team.ru/repo/montserrat/events-front)

Фронтенд сайта Яндекс.События

- Тестинг: https://testing.events.spec-promo.yandex.ru/
- Продакшен: https://events.yandex.ru/

Проект представляет собой одностраничное приложение главной страницы.

Страницы с мероприятиями формируются в конструкторе лендингов (проксирование настроено на уровне qloud в тестинге и продакшене).
Локально проксирование не настроено, поэтому при разработке, когда переходим на мероприятие, получаем 404 ошибку.

### Требования

- Nodejs v12

### Быстрый старт

Создать в корне проекта файл `.tvm.json`, который хранит настройки утилиты для раздачи TVM тикетов.
Содержимое файла можно взять у команды разработки.

```bash

# Устанавливаем зависимости
npm run deps

# Запускаем приложение с помощью magicdev
npm run dev
```

Проект становится доступен по адресу: [https://localhost.msup.yandex.ru/](https://localhost.msup.yandex.ru/)


### Мониторинги

Инвайт для вступления в чат с мониторингами: [events-monitoring](https://t.me/joinchat/E6k4fRazsodwGAwMAglrFw).

- Настройки мониторингов находятся в файле `.monitorado.yml`.
О работе с monitorado подробнее можно прочитать [в документации](https://github.yandex-team.ru/toolbox/monitorado).

- [Error Counter](https://error.yandex-team.ru/projects/events-front)
---

Powered by [Project Stub](https://wiki.yandex-team.ru/toolbox/project-stub/)
