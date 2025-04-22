[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/tools/carrier)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/tools/carrier) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/carrier)](https://oko.yandex-team.ru/pkg/@yandex-market/carrier)

# Carrier

## Установка

```bash
npm i -g @yandex-market/carrier --registry=http://npm.yandex-team.ru
```

Для использования провайдера `ya` требуется настроить себе `yatool`. Подробнее в [документации](./wiki/install.md).

## Использование

```bash
carrier --help
carrier --version
carrier [indent] [--locks ...<locks>] [--modules ...<modules>] [--install <install>] [--provider <provider>] [--custom <custom>]
carrier [indent] [--locks ...<locks>] [--show]
```

* `indent` - название бандла
* `locks` - список лок-файлов, указывается через пробел
* `modules` - список node_modules, указывается через пробел
* `install` - скрипт, который надо запускать для установки модулей
* `provider` - провайдер для сохранения и загрузки бандлов. В текущий момент доступен только `ya`
* `custom` - дополнительные параметры в формате JSON
* `version` - выводит версию carrier'а и выходит
* `show` - выводит параметры бандла и выходит

Все параметры можно описать в файле `.carrierrc`, [см пример](./.carrierrc)

## Что это такое

Carrier реализует 2 сценария:

### Установка из бандла

1. Рассчитывается sha1-хеш от суммы всех указанных в конфиге лок-файлов
2. Если бандл с нужным хешом, неймспейсом и параметрами окружения найден, то он скачивается и распаковывается

### Чистая установка

Если не найден сохранённый бандл текущих зависимостей:

1. carrier делает чистую установку зависимостей (по-умолчанию через `npm ci`)
2. Все указанные `node_modules` упаковываются в бандл `modules.tar.gz`
3. Рассчитывается sha1-хеш от суммы всех указанных в конфиге лок-файлов
4. Сохраняется бандл с рассчитанным хешом, неймспейсом (indent) и параметрами окружения (версия модулей, платформа
   клиента)

----

В текущий момент доступен только провайдер `ya`, который использует yatool для того чтобы сохранять и загружать бандл в
виде sandbox-ресурса. В CI для этого используется специальный пакет `yandex-fakeya`

## Провайдер `ya`

Использует yatool для загрузки и скачивания ресурсов sandbox. В качестве дополнительных параметров можно передать в
custom тип ресурса, например `{"resourceType": "MARKET_FRONT_CARRIER_BUNDLE"}`.

## Инвалидация кеша

Для инвалидации кеша можно найти нужный ресурс в сендбоксе по хешу и удалить его. Стоит обратить внимание, что,
вероятнее всего, ресурсов с одним хешом будет 2 - для ubuntu и для mac. Подробнее в [документации](./wiki/invalidate.md)
