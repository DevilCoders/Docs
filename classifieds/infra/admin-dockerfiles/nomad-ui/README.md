# nomad-ui

## Исходный код и релизы
https://github.com/jippi/hashi-ui/releases/

## Как обновлять
1. Новую версию hashi-ui-linux-amd64 кладем в files/usr/local/bin/

2.
Сборка в teamcity:
- открываем [сборку](https://t.vertis.yandex-team.ru/viewType.html?buildTypeId=VertisAdmin_HashiUi_HashiUi)
- нажимаем run
- успешная сборка запустит деплой в тестинг
- для деплоя в прод используем [стандартные инструменты](https://docs.yandex-team.ru/classifieds-infra/deploy/quick-start#deploj)


Ручной способ:
-  собираем и пушим новый docker образ `APP_VERSION=<version> make build push`
-  деплоим в [шиву](https://docs.yandex-team.ru/classifieds-infra/deploy/quick-start#deploj)
