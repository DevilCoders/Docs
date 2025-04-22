# Корневой package.json

Тут храним все зависимости проекта.

## Команды

* `lint:js` - запуск eslint
* `lint:css` - запуск stylelint
* `lint:spelling` - запуск yaspeller (проверка орфографии)
* `lint` - запуск всех линтеров
* `lint:fix` - запуск всех линтеров с автоисправлением ошибок (последнее работает только для eslint)
* `grpc:generate` - генерация [js-кода](https://developers.google.com/protocol-buffers/docs/reference/javascript-generated#commonjs-imports) из proto-файлов пакета schema-registry.
  При вызове нужно передать в ENV-переменной `PROTOFILE` имя файла относительно директории `node_modules/@vertis/schema-registry/proto`.
  Пример: `PROTOFILE=shiva/types/error/error.proto npm run grpc:generate`.
  Сгенеренные файлы будут лежать в `internal-core/server/resources/grpc-generated/*`.
* `install-ssl-cert` - скачивание ssl-сертификата, используемого для локальной разработки
* `update-hosts` - добавление в файл `/etc/hosts` домена для локальной разработки
