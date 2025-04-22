# tap-internal-components 🚀

Общие компоненты для использования в турбоаппах внутри Яндекса.

## Установка

Для установки пакета следует выполнить в корне репозитория:
```bash
npx lerna add @yandex-int/tap-internal-components --scope=<package-name>
```
где `<package-name>` - название пакета, куда нужно установить `tap-internal-components`.

## Документация

- [helpers](./src/helpers/README.md)

## Деплой

Вспомогательный метод `login` использует специальную страницу для закрытия вкладки,
в которой происходила авторизация.
Эта страница [проксируется](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tap-production/upstreams/list/helpers-return-to-app/show/) из s3 с домена `helpers.tap.yandex.ru`.
Поэтому при изменении этой страницы необходимо залить в s3 новую версию.

## Поддерживаемые браузеры

Для поддержки старых браузеров требуются полифиллы для некоторых фич:
 * [`fetch`](https://github.com/github/fetch)
 * [`URLSearchParams`](https://github.com/jerrybendy/url-search-params-polyfill)

| Browser        | Поддерживаемая версия |
| -------------- | --------------------- |
| Yandex Browser | `>=` 17.0             |
| iOS Safari     | `>=` 10.0             |
| ChromeAndroid  | `>=` 51.0             |
| Samsung        | `>=` 9.0              |
| OperaMobile    | `>=` 60.0             |
| Chrome         | `>=` 72.0             |
| Firefox        | `>=` 78.0             |
| Edge           | `>=` 85.0             |
| Safari         | `>=` 10.0             |
| Opera          | `>=` 71.0             |
