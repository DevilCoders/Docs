# Сервис с вебхуками для автоматизации релизов TAP

Список веб-хуков:

* `POST /ready-for-production` – отправляет релиз выкатываться в продакшн, закрывает тикеты. Вызывается при переводе релизного тикета в статус `Ready for Production`.
* `POST /ready-for-prestable` – отправляет релиз выкатываться в престейбл. Вызывается при переводе релизного тикета в статус `Ready for Prestable`.

## Разработка

Устанавливаем зависимости:
```bash
npx lerna bootstrap --scope @yandex-int/tap-webhooks --include-filtered-dependencies
```

Для локальной разработки запускаем скрипт:
```bash
npx lerna run start --scope @yandex-int/tap-webhooks --stream
```

API становится доступно по локальному адресу [http://localhost:8080](http://localhost:8080).
Приложение автоматически перезапустится при изменениях в коде.
