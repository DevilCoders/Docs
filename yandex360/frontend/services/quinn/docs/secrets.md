# Секреты

Секреты не должны храниться в репозитории. Для хранения секретов используем [секретницу](https://yav.yandex-team.ru/secret/sec-01cscg50qywb10sgyksm0gnhaz). В репозитории хранится только `secrets.example.json`, повторяющий схему. Он так же используется в тестах в CI — копируется в `secrets.json`.

При обновлении секретов нужно обновить example, если меняется схема, обновить версию в секретнице, после чего скопировать их в [qloud-secrets](https://platform.yandex-team.ru/secrets/secret.quinn-secrets) — именно оттуда они прорастают при деплое.

## разработка

Стянуть на дев-машинку последнюю версию секретов можно с помощью `make -C server secrets` (входит в общий `make prepare`). На машинке должна быть установлена `yav` ([документация](https://vault-api.passport.yandex.net/docs/#yav)).

## токены xiva

Выпускать могжет "Менеджер Xiva" [сервиса](https://abc.yandex-team.ru/services/mail/), создавать и отзывать токены [тут](https://push.yandex-team.ru/docnew/console.html#services) ([инструкция для отзыва](https://wiki.yandex-team.ru/yxiva/komprometacija-tokenov/#samostojatelnyjjotzyvtokena)).
