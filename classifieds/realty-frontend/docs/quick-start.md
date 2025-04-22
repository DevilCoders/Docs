# Быстрый старт

Для настройки используется [ansible](https://docs.ansible.com).

## Настройка

Ставим ansible - [инструкция по установке](./ansible-install.md).

Добавляем ssh-ключ в ssh-агента:
```
ssh-add
```

Ставим arc, маунтим яндексовую монорепу - [дока по arc](https://docs.yandex-team.ru/devtools/intro/quick-start-guide).

Далее все делается в монорепе фронта Недвижимости.
Она располагается по пути `arcadia/classifieds/realty-frontend/`

Запускаем ansible:
```
make ansible-local
```

> Если установка зависимостей уже осуществлялась, то можно запустить только конфигурацию:<br>
`make ansible-local-configure`
<br>или наоборот, только установку зависимостей:<br>
`make ansible-local-install`

После установки нужно перезапустить терминал или выполнить `source ~/.zshrc` или `source ~/.bash_profile`, чтобы nvm и node были доступны.

## Запуск

```
cd <project_dir>
make deps
make webpack
make start-local (выведет url на который можно зайти)
```

> Команда `make webpack` полностью собирает проект, что может быть очень долго.
Подробнее про сборку [тут](./webpack.md).

Для упрощения жизни рекомендую добавить себе алиасы в .zshrc/.bash_profile
```
alias sl="make start-local"
alias sld="make start-local-debug"
alias wwbc="make webpack-watch bundle=common"
alias wbc="make webpack bundle=common"
```

Настроить инструменты для генерации компонентов, в зависимости от IDE. Подробнее [тут](../packages/utils/codegen/readme.md).

## SSL-сертификат

> **Для базовый настройки окружения ничего обновлять не надо**

SSL-сертификат лежит в [секретнице](https://yav.yandex-team.ru/secret/sec-01dh68da2kx3t7r5c6sdqxjnw5/explore/versions).

Если его нужно обновить, то
- заходим в [crt](https://crt.yandex-team.ru/certificates/?cr-form=1&cr-form-type=host&cr-form-ca_name=InternalCA&cr-form-abc_service=119)
- в соседней вкладке заходим на локальный url (`make start-local`)
и смотрим в DevTools Security на какие домены выписан сертификат
- копируем нужные домены из DevTools Security, добавляем новые/редактируем, если нужно
- жмякаем "Заказать"
- скачиваем `.pem` сертификат и кладем его содержимое в секретницу.
[Как работать с секретницей](https://wiki.yandex-team.ru/passport/yav-usage/).
При этом в новой версии секрета должен быть только один ключ с названием `cert`.

## FAQ

**Q:** Почему бы не поднять Nginx в Docker и избавиться от ручной настройки? <br>
**A:** Мы используем unix socket'ы, а они не работают в схеме Docker[Nginx] <-> MacOS[Node].

**Q:** Почему бы тогда не использовать docker-compose и запустить Node и Nginx в Docker? <br>
**A:** Наши бекенды используют IPv6, который не работает в Docker на MacOS.
