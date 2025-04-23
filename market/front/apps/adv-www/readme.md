# adv-front [![Build Status](https://drone.yandex-team.ru/api/badges/advertising/adv-front/status.svg)](https://drone.yandex-team.ru/advertising/adv-front)

Ссылка на [wiki](https://wiki.yandex-team.ru/users/aisaev188/adv-partner/) проекта.

Благодаря платформе [magicdev](https://github.yandex-team.ru/project-stub/magicdev#Что-это-зачем-и-как-этим-пользоваться), проект разрабатывается локально.

Для работы потребуется _Node.js 12_ – устанавливаем его по необходимости:

```bash
brew install nvm
nvm install 12
```

Далее устанавливаем зависимости и запускаем проект:

```bash
npm run deps

# Выгрузить ключи из танкера
npm run i18n

# Magicdev запросит ваш пароль, чтобы запустить на 443 порту
npm run dev
```

Проект становится доступен по адресу:
https://localhost.msup.yandex.ru/partners/

## Если нужно принудительно сбросить кеш статики (изменения в скриптах или стилях)

Нужно поменять путь в configs/defaults.js - поле static.host. Пока только так :(

## Дополнительная настройка

-   [Интеграция с Drone CI](docs/drone.md)
-   [Автоматическая сборка docker-образа и выкладка в Qloud](docs/qloud.md)
-   [Автоматическая перезагрузка страниц в браузере по изменению файлов](docs/browser-sync.md)

## Tunneler

Для отладки приложения с других устройств используется [Tunneler](https://wiki.yandex-team.ru/q/devops/tunneler/).

Запустить его можно командой:

```bash
./tunel.sh ekb-tunneler.ldev.yandex-team.ru 443 1
```

Проект становится доступен по адресу:
https://<username>-1-ekb.ldev.yandex.ru/adv/
