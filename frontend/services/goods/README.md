# Товарная вертикаль

[Сервис](https://yandex.ru/products/?text=iphone) для сравнения и выбора товаров.

[Плагин для браузера SERP](https://github.yandex-team.ru/devexp/serp-browser-ext) — швейцарский нож для работы с поисковыми проектами.

## Запуск

1. Должен использоваться `node` версии, указанной в [.nvmrc](./.nvmrc).

2. Установка зависимостей

    ```bash
    npm ci
    ```

3. Сборка проекта

    ```bash
    npm run build
    ```

4. Запуск dev-сервера

    ```bash
    npm run start
    ```

    или
    ```bash
    npm run start:public
    ```

### Запуск в testing режиме

```bash
npm ci
npm run build:testing:local # сборка в testing, но для локального запуска
npm run testing
```

## Query-параметры
- [json=1](https://yandex.ru/products/?text=iphone&json=1) — посмотреть данные от бекенда для шаблонизации страницы
- [dump_eventlog_only=1](https://yandex.ru/products/?text=iphone&dump_eventlog_only=1) — посмотреть только eventlog
- [dump=eventlog](https://yandex.ru/products/?text=iphone&dump=eventlog) — посмотреть eventlog под страницей
- [json_dump_requests=REPORT_RENDERER](https://yandex.ru/products?text=iphone&json_dump_requests=REPORT_RENDERER) — посмотреть ответы источников для REPORT_RENDERER
- [i-m-a-hacker=1](https://yandex.ru/products/?text=iphone&i-m-a-hacker=1) — эмулировать внешнюю сеть
- [promo=nomooa](https://yandex.ru/products/?text=iphone&promo=nomooa) - скрыть жука
- [exp_flags=validate_counters](https://yandex.ru/products/?text=iphone&exp_flags=validate_counters) — выводить логи баобаба
- [exp_flags=analytics_disabled=0&_ym_debug=1](https://yandex.ru/products/?text=iphone&exp_flags=analytics-disabled=0&_ym_debug=1) — выводить логи метрики

## Оглавление

* [Компоненты](src/components/README.md)
* [Redux Store](src/store/README.md)
* [Схемы нормализации данных](src/schema/README.md)
* [Баобаб-счётчики](src/utils/baobab/README.md)
* [Эксперименты](expflags/README.md)
* [Гермиона-тесты](tests/hermione/README.md)
* [Apphost](src/apphost/README.md)
* [Жучок](src/utils/butterfly/README.md)
