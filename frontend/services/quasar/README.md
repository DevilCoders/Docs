# Пользовательский интерфейс для управления Умным домом и настройки колонок

Доступен в ПП по кнопке Устройства

Production: **[https://yandex.ru/quasar/](https://yandex.ru/quasar)**  
Release Candidate: **[https://rctemplates-shared.hamster.yandex.ru/quasar](https://rctemplates-shared.hamster.yandex.ru/quasar/)**  

## Установка
`npm ci`

## Локальный запуск
`npm start`

UI будет доступен по URL: **[https://local.yandex.ru:3443/quasar](https://local.yandex.ru:3443/quasar)**

С созданием туннеля для внутренней сети:

`npm start -- --public`

## Скрипты для разработки
### Скрипт для оптимизации анимированных SVG
`tools/svg.js`

1. Удаляет неиспользуемые классы CSS и атрибуты ID
2. Сокращает названия классов CSS и анимаций
3. Устанавливает уникальные названия классов CSS и анимаций с префиксом
4. Прогоняет через SVGO

Использование:

`node ./tools/svg.js <path> <prefix>`

- `<path>` — путь до файла SVG
- `<prefix>` — префикс, который будет использован для генерации CSS-классов

Пример:

`node ./tools/svg.js src/components/blocks/some/assets/image.svg some-svg`

### Скрипт для прогона строк i18n через типограф

`tools/typograf.js`

Проставляет неразрывные пробелы. Использование:

`node ./tools/typograf.js <path>`

В качестве пути `<path>` можно передать путь до файла компонента или директории с компонентами.

Пример:

`node ./tools/typograf.js src/components/blocks/some/index.tsx`


## Полезная информация

- Про apphost можно почитать здесь https://doc.yandex-team.ru/apphost/ и здесь https://wiki.yandex-team.ru/search-interfaces/infra/dev-at-apphost
- TS Пакет с тайпингами и API для работы с контекстом апхоста: https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/frontend-apphost-context
- Про Archon https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/archon
- Про Kotik https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/kotik
