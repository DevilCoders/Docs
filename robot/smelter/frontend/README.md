# Фронтенд Медиамониторинга

[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=robot/smelter/frontend&vcs=arc)](https://oko.yandex-team.ru/arc/robot/smelter/frontend)

Фронтенд сервиса [Медиамониторинг](https://wiki.yandex-team.ru/robot/mediamonitoring/).
Используемые технологии: React.js + TypeScript + Next.js

## Подготовка
Для работы потребуется Node.js v16.
Рекомендуемый способ установки конкретной версии Node.js – [nvm](https://github.com/nvm-sh/nvm).
Есть версия для [brew](https://formulae.brew.sh/formula/nvm).

```bash
nvm install
nvm use
```

Установка зависимостей
```bash
npm ci
```

## Сборка

production
```bash
npm run build
```

testing
```bash
npm run build:testing
```

## Запуск
Запуск dev-сервера
```bash
npm run dev
```

Запуск production-сборки
```bash
npm run build
npm run start
```

Запуск testing-сборки
```bash
npm run build:testing
npm run start
```

## Проверки
Линтер
```bash
npm run lint
```

## Деплой в testing
Пока в ручном режиме.

```bash
npm run build:testing
npm run upload
```
- Указать id полученного ресурса:
  - [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/smelter-testing-frontend/files)
- Активировать новую версию

## Деплой в production
Пока в ручном режиме.

```bash
npm run build
npm run upload
```
- Указать id полученного ресурса:
  - [production](https://nanny.yandex-team.ru/ui/#/services/catalog/smelter-production-frontend/files)
- Активировать новую версию
