# Package hiring-express-host-aliases

Пакет для добавления алиаса в /etc/hosts

## Использование

```bash
~$ npm install --save-dev @yandex-taxi/fm-hiring-express-host-aliases
```

```javascript
addAliases([
    {host: 'some.test', ip: '127.0.0.1'},
    {host: 'my.app.dev.txi.yandex.ru', ip: '127.0.0.1'},
], 'service-name');
```

## Паблишинг
Для упрощения жизни установите np:
`npm install --global np`

Перейдите в папку `packages/hiring-express-host-aliases` и запустите утилиту:
`np`

1. Пройдите шаги;
2. Сделайте пуш в репу новой версии.
