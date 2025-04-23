Project related utilities
===

# protogen
Инструмент для генерации Swift Codable-моделей для JSON-формата Protobuf-моделей.<br/>
Исполняемый Ruby-скрипт.
Для работы рекомендуется версия Ruby 2.5.5 или выше.

## Требования
Для работы необходимы следующие компоненты:
* protobuf компилятор `protoc`
* плагин `protoc-gen-swiftjson` для `protoc` (внутренний инструмент Яндекс.Вертикалей)
* основной репозиторий proto-моделей `schema-registry`

### protoc
Установка:
* Используя Homebrew `brew install protobuf`
* Скачать бинарник https://github.com/protocolbuffers/protobuf/releases
  * Распаковать в `~/.bin` (полный путь будет `~/.bin/protoc`)
  * Добавить директорию `$HOME/.bin/protoc/bin` в `$PATH` (например, добавить `export PATH="$HOME/.bin/protoc/bin:$PATH` в `~/.profile`)

### Плагин `protoc-gen-swiftjson`
Плагин на Ruby для `protoc` для генерации моделей.

```bash
git clone git@github.com:YandexClassifieds/mobile-libraries-ios.git
```

Далее надо инициализировать плагин – выполнить инструкции по подготовке из `protoswiftjson/README.md`

### Репозиторий `schema-registry`
Основной репозиторий моделей для всех сервисов Яндекс.Вертикалей.

```bash
git clone git@github.com:YandexClassifieds/schema-registry.git
```

### Realty proto-модели
У backend Недвижимости есть набор локальных для проекта моделей.

```bash
git clone git@github.com:YandexClassifieds/realty.git
```

Сами модели лежат в `realty/realty-model/src/main/proto`.<br/>
Для работы им нужен основной репозиторий моделей `schema-registry`.

## Использование

Для упрощения использования все репозитории можно положить на один уровень:
```
* repos
  * mobile-realty-client-ios
  * mobile-libraries-ios
  * schema-registry
  * realty
```

Для генерации моделей только из основного репозитория:
```bash
./Utils/protogen -p '../mobile-libraries-ios/protoswiftjson' -S '../schema-registry/proto' -i './YREPackages/YREWebModels/Sources/Protobuf.yml' -o './YREPackages/YREWebModels/Sources/Protobuf' -f
```

Для генерации моделей из realty репозитория:
```bash
./Utils/protogen -p '../mobile-libraries-ios/protoswiftjson' -I '../schema-registry/proto' -S '../realty/realty-model/src/main/proto' -i './YREPackages/YREWebModels/Sources/Realty.yml' -o './YREPackages/YREWebModels/Sources/Realty' -f
```

Формат YAML-файла для выборки моделей из репозиториев см. в `mobile-libraries-ios/protoswiftjson/README.md`
