# hermione-surfwax-router

Плагин для [hermione](https://github.com/gemini-testing/hermione), работающий в связке с сервисом [surfwax](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/surfwax). Отвечает за переопределение endpoint'а с surfwax балансера на адрес selenoid-хоста с поднятым браузером. Подмена endpoint'а выполняется после поднятия сессии на событие `SESSION_START`. Данный плагин позволяет уменьшить нагрузку на surfwax-балансер. Работает только в CI на агентах с прямым доступом к selenoid-хостам.

## Установка

```bash
$ npm install @yandex-int/hermione-surfwax-router --registry=http://npm.yandex-team.ru
```

## Использование

Необходимо подключить плагин в конфиге `hermione`:

```js
module.exports = {
    // ...

    plugins: {
        '@yandex-int/hermione-surfwax-router': {
            enabled: true, // Включить/выключить плагин. По умолчанию включен.
            surfwaxHostname: 'sw.yandex-team.ru', // Хост surfwax, используется для того, чтобы определить нужно ли подменять endpoint для сессии или нет. По умолчанию `sw.yandex-team.ru`
        }
    },
    // ...
};
```
