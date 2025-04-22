# Планировщик задач для MRC

Technologies:
* [React](https://github.yandex-team.ru/maps/maps/blob/dev/docs/react.md)
* [Typescript](https://github.yandex-team.ru/maps/maps/blob/dev/docs/typescript.md)
* [Webpack](https://github.yandex-team.ru/maps/maps/blob/dev/docs/webpack.md)

## Установка


### Разработка локально

#### Требования к системе

- Ключи ssh/gpg с локальной машины на [staff](https://staff.yandex-team.ru/)
- node.js (для избежания проблем совместимости - версии 8)

#### Установка

```
npm ci
npm run local-setup
```

После этого:
* в /etc/hosts добавьте ```127.0.0.1 mrc-planner.dev.yandex.ru```
* добавьте созданный сертификат .ssl/ssl.crt в доверенные
  * на Mac для этого нужно открыть Keychain, добавить сертификат в связку "Система" и в свойствах сертификата изменить параметры использования на "Всегда доверять".

#### Запуск

```
npm run dev
```

Откройте `https://mrc-planner.dev.yandex.ru:8081` в браузере.

### Новый патч

Для того чтобы выкатить патч, в который войдут все текущие комиты из дева, нужно запустить команды

```
npm run patch
```

Новый патч появится в гитхабе в разделе releases. В [тестинг](https://mrc-planner.tst.maps.yandex-team.ru) он выкатывается автоматически хуком (обычно в течение 15-20 минут).

Если по какой-то причине этого не произошло, можно подтолкнуть патч до тестинга руками.

```
npm run release-testing
```

### Новый минор

С минорами то же самое, но команда немного другая:

```
npm run minor
```

### Выкатка в прод

После того как тестировщики протестировали все фичи в новом патче и в статусах задач в стартреке, относящихся к текущему патчу, стоит "Протестировано", можно выкатывать свежую версию в [продакшн](https://platform.yandex-team.ru/projects/maps/front-mrc-planner/production)
