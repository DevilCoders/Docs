# safe-www [![Build Status](https://drone.yandex-team.ru/api/badges/stardust/safe-www/status.svg)](https://drone.yandex-team.ru/stardust/safe-www)

* [Cборка релиза](https://a.yandex-team.ru/projects/frontend/ci/releases/timeline?dir=frontend%2Fservices%2Fsafe-www&id=release)

Благодаря платформе [magicdev](https://github.yandex-team.ru/project-stub/magicdev#Что-это-зачем-и-как-этим-пользоваться), проект разрабатывается локально.

Для работы потребуется _Node.js 6_ – устанавливаем его по необходимости:

```bash
brew install nvm
nvm install 6
```

Далее устанавливаем зависимости и запускаем проект:

```bash
npm run deps

# Magicdev запросит ваш пароль, чтобы запустить на 443 порту
npm run dev
```

Проект становится доступен по адресу:  
https://localhost.msup.yandex.ru/safe/

## Дополнительная настройка

* [Автоматическая перезагрузка страниц в браузере по изменению файлов](docs/browser-sync.md)
