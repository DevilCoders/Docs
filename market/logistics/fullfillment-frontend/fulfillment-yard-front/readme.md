# Клиент для электронной очереди
#### Установка пакетов
- Ставим LTS node.js (12.18.3 на момент написания) https://nodejs.org/en/
- Пишем `npm i`

#### Запуск на моках
- `npm run mock`

#### Запуск
- `npm run start`

#### Запуск на тестинге
- `npm run start:prest`

#### Запуск с кастомным хостом бэка
- `API_HOST=<тут ваш хост> npm run start`

#### Запуск линтера
- `npm run lint`

#### Иногда надо запустить фронт не на 8080
- `PORT=<ваш порт> npm run start`

## Структура папок
### `routes` - папка с конкретными страницами
#### `<page>` Содержит в себе (все что относится к странице)
- `hooks.ts` - кастомные хуки, чаще всего обращения к бэку и поллинг
- `<page>-api.ts` - набор функций для обращения к бэку, инициализируется лениво 
в хуке `useState` на старте страницы. (типизация функций происходит динамически
на основе моков)
- `<page>-page.tsx` - сама страница и функции для неё
- `components` - папка с компонентами для этой конкретной страницы
- `types` - папка с типами для этой конкретной страницы
- `mock.ts` - набор наиболее больших моков бэка
- `index.ts` - доступ для внешних файлов
- `<inner-page>` - если есть вложенность по `route`
#### `router.tsx` - точка входа для роутов
### `__spec__` - юниты
### `assets` - статика, копируется вебпаком as is
### `components` -  общие компоненты
### `constants` - общие константы
### `hooks` - общие хуки
### `lib` - общие функции и дефолтные функции (для композиции)
#### `api` - дефолтные функции для апи
#### `utils` - воспомогательные функции
### `types` - общие типы

## Автотесты
### Конфигурация

[Конфиг файл](./configs/hermione.js)
### Запуск
```bash
# Запуск автотестов
npm run test:hermione

# Запуск автотестов в удаленном селениуме
npm run test:hermione:grid

# Обновление скриншотов
test:hermione:update
```

### Полезные ссылки
* [Selenium: инфраструктура предоставления браузеров](https://wiki.yandex-team.ru/selenium/);
* [Report](./hermione-report/index.html) (Доступен после запуска)
